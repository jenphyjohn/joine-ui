

<template>
  <div class="pull-chheight wel-contailer">
    <div class="banner-text">
      <h2>Joine 微服务开发平台</h2>
      <span align="center">
        <img src="https://img.shields.io/badge/Spring%20Cloud-EdgwareSR4-orange.svg" alt="Coverage Status">
        <img src="https://img.shields.io/badge/Spring%20Boot-1.5.13-blue.svg" alt="Downloads">
        <img src="https://img.shields.io/npm/v/npm.svg" alt="Version">
        <img src="https://img.shields.io/hexpm/l/plug.svg" alt="License">
      </span>
      <br/>
      <span>
          <el-collapse v-model="activeNames">
            <el-collapse-item title="项目特点" name="1">
              <div>
                <div>Spring Cloud 最完整运用 </div>
                <div>深度定制兼容 1.0 、 2.0</div>
                <div>覆盖常见的业务使用场景</div>
              </div>
            </el-collapse-item>
            <el-collapse-item title="快速开发" name="2">
              <div>
                <div>微服务快速开发平台Joine</div>
                <div>业务实现、监控落地、生产应用</div>
              </div>
            </el-collapse-item>
            <el-collapse-item title="公司官网" name="3">
              <a href="https://join-e.tech/" target="_blank">
              <div>基于Spring Cloud Gateway</div>
              <div>基于Spring Cloud Finchley.SR1</div>
              <div>基于Spring Boot 2.0.4.RELEASE</div>
              <div>基于开源LCN 分布式事务解决方案深度定制</div>
              </a>
            </el-collapse-item>
          </el-collapse>
        </span>
      <span>
        </span><br>
      <span :class="['actor',{typeing:isText}]">{{text}}</span>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'wel',
  data() {
    return {
      activeNames: ['1', '2', '3', '4'],
      DATA: [],
      text: '',
      actor: '',
      count: 0,
      isText: false
    }
  },
  computed: {
    ...mapGetters(['website'])
  },
  created() {
    this.DATA = this.website.wel.list
    this.actor = this.DATA[this.count] || ''
    setTimeout(() => {
      this.isText = true
      this.setData()
    }, 2000)
  },
  methods: {
    getData() {
      if (this.count < this.DATA.length - 1) {
        this.count++
      } else {
        this.count = 0
      }
      this.isText = true
      this.actor = this.DATA[this.count]
    },
    setData() {
      let num = 0
      let count = 0
      let active = false
      const timeoutstart = 5000
      const timeoutend = 1000
      const timespeed = 10
      setInterval(() => {
        if (this.isText) {
          if (count === this.actor.length) {
            active = true
          } else {
            active = false
          }
          if (active) {
            num--
            this.text = this.actor.substr(0, num)
            if (num === 0) {
              this.isText = false
              setTimeout(() => {
                count = 0
                this.getData()
              }, timeoutend)
            }
          } else {
            num++
            this.text = this.actor.substr(0, num)
            if (num === this.actor.length) {
              this.isText = false
              setTimeout(() => {
                this.isText = true
                count = this.actor.length
              }, timeoutstart)
            }
          }
        }
      }, timespeed)
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.wel-contailer {
  position: relative;
}
.banner-text {
  position: relative;
  padding: 0 20px;
  font-size: 20px;
  text-align: center;
  color: #333;
}
.banner-img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  display: none;
}
.actor {
  height: 250px;
  overflow: hidden;
  font-size: 18px;
  color: #333;
}

.actor:after {
  content: "";
  width: 3px;
  height: 25px;
  vertical-align: -5px;
  margin-left: 5px;
  background-color: #333;
  display: inline-block;
  animation: blink 0.4s infinite alternate;
}

.typeing:after {
  animation: none;
}

@keyframes blink {
  to {
    opacity: 0;
  }
}
</style>
