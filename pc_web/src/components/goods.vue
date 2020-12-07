<!--这个界面用来：在用户d登录之后，展示视频流-->


<template>
  <div>
    <el-row>
      <el-col :span="5">
        <div class="grid-content-userInfo bg-purple-dark-userInfo"></div>
      </el-col>
      <el-col :span="14">
        <div class="grid-content-userInfo bg-purple-dark-userInfo">

          <!--          <el-row>-->
          <!--          </el-row>-->

          <!--左边-->
          <el-col :span="18" class="grid">

            <div class="demo-img-userPhoto">
              <img :src="'data:image/jpeg;base64,'+ flow_img"
                   style="width: 640px;height: 480px; margin-right: 200px"></img>
            </div>

            <div class="demo-input-userName" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="10" style="text-align: right">输入待检测人name/ID:
                </el-col>
                <el-col :span="12">
                  <el-input
                      :disabled="false"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      placeholder="name(选填)"
                      v-model="textArea_specific_user">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-button-signInOut" style="margin-top: 10px;">
              <el-button type="primary" style="margin: 5px" @click.prevent="start_detc()">开始检测</el-button>
              <el-button type="primary" style="margin: 5px" @click.prevent="stop_detc()">暂停检测</el-button>
            </div>

          </el-col>
          <!--右边-->
          <el-col :span="6" class="grid">

            <!--            <div class="demo-img-userPhoto">-->
            <!--              <img :src="'data:image/jpeg;base64,'+ flow_img_moment"-->
            <!--                   style="width: 640px;height: 480px; margin-right: 200px"></img>-->
            <!--            </div>-->

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="12">
                  <div style="text-align: right">
                    检测到的人数 :
                  </div>
                </el-col>
                <el-col :span="12">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_num">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="12">
                  <div style="text-align: right">
                    姓名 :
                  </div>
                </el-col>
                <el-col :span="12">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_name1">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="12">
                  <div style="text-align: right">
                    ID :
                  </div>
                </el-col>
                <el-col :span="12">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_id">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="12">
                  <div style="text-align: right">
                    group ID :
                  </div>
                </el-col>
                <el-col :span="12">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_groupID">
                  </el-input>
                </el-col>
              </el-row>
            </div>


          </el-col>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="grid-content-userInfo bg-purple-dark-userInfo"></div>
      </el-col>
    </el-row>

    <!--        提示信息行-->
    <el-row>
      <el-col :span="5">
        <div class="grid-content-goods bg-purple-dark-goods"></div>
      </el-col>
      <el-col :span="14">
        <div class="grid-content-goods bg-purple-dark-goods">
          <h3 style="margin: 3px">
            注意！本网站仅用作人脸检测和识别的展示，并不代表正式场景<br/>
          </h3>
          <br>
          <h3 style="margin: 2px">
            网站似乎出问题了？请联系 tangjiank@enn.cn<br/>
          </h3>

        </div>
      </el-col>
      <el-col :span="5">
        <div class="grid-content-goods bg-purple-dark-goods"></div>
      </el-col>
    </el-row>

    <br>
  </div>
</template>
<style>
/*搜索行，样式全局影响，要特殊命名*/
.bg-purple-dark-userInfo {
  background: Transparent;
}

.grid-content-userInfo {
  border-radius: 0px;
  min-height: 30px;
}

.bg-purple-dark-goods {
  background: Transparent;
}

.grid-content-goods {
  border-radius: 0px;
  min-height: 30px;
}

.bg-purple-dark-goods2 {
  background: #E5E5E5;
}

.grid-content-goods2 {
  border-radius: 0px;
  min-height: 100px;
}
</style>
<script>
export default {
  created() {
    this.initUserInfo();
  },
  data() {
    return {
      fake_ret: {
        "result": 0,
        "message": "SUCCESS",
        "image": "123",
        "faces": [{
          "user_id": "10098440",
          "group_id": "staff",
          "user_info": "康佳慧",
          "box": [390, 167, 545, 322],
          "distance": 0.34566974479547136
        }]
      },
      textArea_specific_user: '',
      textArea_user_num: '',
      textArea_user_name1: '',
      textArea_user_id: '',
      textArea_user_groupID: '',
      flow_img: '',
      flow_img_moment: '',
      test_model: false,
      stop_detc_flag: false,   // 为真时，停止向服务器的请求
      intervalID:'', // 定时任务ID
    };
  },
  methods: {

    // 界面进来就会根据localStorage存储的当前用户信息，初始化用户详情
    initUserInfo() {

      // this.$message({
      //   showClose: true,
      //   type: 'success',
      //   message: '服务器连接畅通，随时可以开车'
      // });

      this.$message({
        showClose: true,
        type: 'success',
        message: '服务器畅通,随时可以发车~'
      });

    },

    async start_detc() {
      let _this = this;
      while (!_this.stop_detc) {
        await this.$http.get("getImgFlow").then(result => {
          var result = result.body;
          if (result.message === 'SUCCESS') {
            this.flow_img = result.image;
            this.textArea_user_num = result.faces.length;
            if (this.textArea_user_num < 1) {
              this.textArea_user_name1 = '';
              this.textArea_user_id = '';
              this.textArea_user_groupID = '';
            } else {

              this.textArea_user_name1 = result.faces[0].user_info;
              this.textArea_user_id = result.faces[0].user_id;
              this.textArea_user_groupID = result.faces[0].group_id;
            }
          } else {
            // this.stop_detc_flag = true;
          }
        });

      }
    },

    stop_detc() {
      let _this = this;
      _this.stop_detc = true;
    },


    // start_detc() {
    //   let _this = this;
    //   this.intervalID = '';
    //   this.intervalID = setInterval(function(){
    //     _this.start_detc_1();
    //   }, 150);
    // },

    // stop_detc() {
    //   clearInterval(this.intervalID); // 清除定时器
    //   this.intervalID = '';
    // },


    start_detc_1() {
      if (this.test_model) {
        this.flow_img = this.fake_ret.image;
        this.textArea_user_num = this.fake_ret.faces.length;
        this.textArea_user_name1 = this.fake_ret.faces[0].user_info;
        this.textArea_user_id = this.fake_ret.faces[0].user_id;
        this.textArea_user_groupID = this.fake_ret.faces[0].group_id;
      } else {
            this.$http.get("getImgFlow").then(result => {
              var result = result.body;
              if (result.message === 'SUCCESS') {
                this.flow_img = result.image;
                this.textArea_user_num = result.faces.length;
                if (this.textArea_user_num < 1) {
                  this.textArea_user_name1 = '';
                  this.textArea_user_id = '';
                  this.textArea_user_groupID = '';
                } else {

                  this.textArea_user_name1 = result.faces[0].user_info;
                  this.textArea_user_id = result.faces[0].user_id;
                  this.textArea_user_groupID = result.faces[0].group_id;
                }
              } else {
                // this.stop_detc_flag = true;
              }
            });
      }
    },







    // 占据末尾的function ，不会被调用，请在它上面添加functions ，
    useless_f() {
      this.$message({
        message: '道路畅通，随时可以开车',
        type: 'success'
      });
    }


  }
};
</script>