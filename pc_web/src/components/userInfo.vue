
<!--这个界面用来：在用户未登录时候进行default展示-->

<template>
    <div>
        <el-row>
            <el-col :span="5">
                <div class="grid-content-userInfo bg-purple-dark-userInfo"></div>
            </el-col>
            <el-col :span="14">
                <div class="grid-content-userInfo bg-purple-dark-userInfo">
                    <!--左边-->
                    <el-col :span="9" class="grid">
                        <div class="demo-img-userPhoto">
                            <img :src="'data:image/jpeg;base64,'+ demoUserImage"
                                 style="width: 200px;height: 200px; margin-right: 200px"></img>
                        </div>

                        <div class="demo-input-userName" style="margin-top: 10px;">
                            <el-row :gutter="2">
                                <el-col :span="10">当前登录用户的用户名:
                                </el-col>
                                <el-col :span="12">
                                    <el-input
                                            :disabled="true"
                                            style="margin-top: -6px;"
                                            type="textarea"
                                            autosize
                                            placeholder="Gust"
                                            v-model="textArea_current_name">
                                    </el-input>
                                </el-col>
                            </el-row>
                        </div>
                        <div class="demo-button-signInOut" style="margin-top: 10px;">
                            <el-button type="primary" style="margin: 5px" @click.prevent="openSignUp()">Sign up</el-button>
                            <el-button type="primary" style="margin: 5px" @click.prevent="handleSignOut()">Sign Out</el-button>
                            <el-button type="primary" style="margin: 5px" @click="dialogFormVisible = true">Sing In / Switch account</el-button>

                            <!-- 登录的弹出界面 -->
                            <el-dialog title="登录" :visible.sync="dialogFormVisible">
                                <el-form :model="form">
                                    <el-form-item label="Name 用户名" :label-width="formLabelWidth">
                                        <el-input v-model="form.userName" placeholder="可选"
                                                  autocomplete="off"></el-input>
                                    </el-form-item>
                                    <el-form-item label="Email 邮箱" :label-width="formLabelWidth">
                                        <el-input v-model="form.email" placeholder="可选" autocomplete="off"></el-input>
                                    </el-form-item>
                                    <el-form-item label="Password 密码" :label-width="formLabelWidth">
                                        <el-input v-model="form.password" placeholder="必填"
                                                  autocomplete="off"></el-input>
                                    </el-form-item>
                                </el-form>
                                <div slot="footer" class="dialog-footer">
                                    <el-button type="primary" @click="dialogFormVisible = false">Cancel</el-button>
                                    <el-button type="primary" @click="dialogFormVisible = false"
                                               @click.prevent="handleSignIn()">OK
                                    </el-button>
                                    <el-button type="primary" @click="dialogForm2Visible = true">Forget your info? 忘记登录信息？
                                    </el-button>
                                </div>
                            </el-dialog>
                            <!-- 找回用户名密码等信息的弹出界面 -->
                            <el-dialog title="Regain your information" :visible.sync="dialogForm2Visible">
                                <el-form :model="form2">
                                    <el-form-item label="用户名" :label-width="formLabelWidth">
                                        <el-input v-model="form2.userName" placeholder="可选"
                                                  autocomplete="off"></el-input>
                                    </el-form-item>
                                    <el-form-item label="邮箱" :label-width="formLabelWidth">
                                        <el-input v-model="form2.email" placeholder="可选" autocomplete="off"></el-input>
                                    </el-form-item>
                                    <el-form-item label="请描述你记得的信息" :label-width="formLabelWidth">
                                        <el-input v-model="form2.lostFoundKey" placeholder="可选"
                                                  autocomplete="off"></el-input>
                                    </el-form-item>
                                </el-form>
                                <div slot="footer" class="dialog-footer">
                                    <el-button type="primary" @click="dialogForm2Visible = false">Cancel</el-button>
                                    <el-button type="primary" @click="dialogForm2Visible = false"
                                               @click.prevent="handleFindUserInfo()">找回登录信息
                                    </el-button>
                                </div>
                            </el-dialog>

                        </div>


                    </el-col>
                    <!--右边-->
                    <el-col :span="14" class="grid">
                        <div class="demo-input-email" style="margin-top: 10px;">
                            <el-row :gutter="2">
                                <el-col :span="7">
                                    <div style="text-align: right">
                                        ID :
                                    </div>
                                </el-col>
                                <el-col :span="15">
                                    <el-input
                                            :disabled="true"
                                            style="margin-top: -6px;"
                                            type="textarea"
                                            autosize
                                            v-model="textArea_current_ID">
                                    </el-input>
                                </el-col>
                            </el-row>
                        </div>

                        <div class="demo-input-phoneNum" style="margin-top: 10px;">
                            <el-row :gutter="2">
                                <el-col :span="7">
                                    <div style="text-align: right">
                                        E-mail :
                                    </div>
                                </el-col>
                                <el-col :span="15">
                                    <el-input
                                            :disabled="true"
                                            style="margin-top: -6px;"
                                            type="textarea"
                                            autosize
                                            v-model="textArea_current_email">
                                    </el-input>
                                </el-col>
                            </el-row>
                        </div>

                        <div class="demo-input-joinTime" style="margin-top: 10px;">
                            <el-row :gutter="2">
                                <el-col :span="7">
                                    <div style="text-align: right">
                                        Sign up time :
                                    </div>
                                </el-col>
                                <el-col :span="15">
                                    <el-input
                                            :disabled="true"
                                            style="margin-top: -6px;"
                                            type="textarea"
                                            autosize
                                            v-model="textArea_current_sginTime">
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


        <!-- 弹出sign up 界面-->
        <el-dialog title="Sign Up/注册" :visible.sync="signUpAble">
            <el-row>
                <el-form :model="formSignUp">
                    <el-form-item label="Email/邮箱:" :label-width="formLabelWidth">
                        <el-input  v-model="formSignUp.email" placeholder="not null/必填"
                                  autocomplete="off" ></el-input>
                    </el-form-item>

                    <el-form-item  label="name/用户名:" :label-width="formLabelWidth">
                        <el-input  v-model="formSignUp.userName" placeholder="not null/必填"
                                  autocomplete="off" ></el-input>
                    </el-form-item>

                  <el-upload
                      action=""
                      multiple
                      :limit="1"
                      accept=".jpg,.jpeg,.png,.gif,.bmp,.pdf,.JPG,.JPEG,.PBG,.GIF,.BMP,.PDF"
                      :on-change="handle_change"
                      :on-remove="handle_remove"
                      :on-exceed="handleExceed"
                      :before-upload="uploadBefore"
                      :auto-upload = "false"
                      :file-list="fileList"
                      list-type="picture">
                    <el-button slot="trigger" size="medium" type="primary"
                               style="float:left; font-size:16px; margin: 10px">点击这里上传人脸图片</el-button>
                    <el-button size="medium" type="primary"
                               style="float:left; font-size:16px; margin: 10px"
                               @click.prevent="takePhoto()">点击这里拍照</el-button>
                    <div slot="tip" class="el-upload__tip" >上传和拍照2选1即可, 仅可上传一张图, 图片类型支持 jpg jpeg png gif  bmp  pdf</div>
                  </el-upload>

                </el-form>
            </el-row>
            <el-row>
                <el-button
                        type="primary"
                        style="float:left; font-size:16px; margin: 10px"
                        @click.prevent="signUp()">Sign Up 注册
                </el-button>
            </el-row>
            <el-row>
                <h4>
                    1:同样的邮箱/用户名只能注册1次<br/>
                    2:密码没有最短长度/大小写/特殊字符限制，但推荐写简单一点<br/>
                    3:后台有IP检测，想恶意刷号会被限制<br/>
                    4:上述三点也许并没有来得及实现，所以.....<br/>
                </h4>
            </el-row>
        </el-dialog>

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
            this.getIp();
            // this.initUserInfo();
            // this.adminView();
        },
        data() {
            return {
                textAreaUserName: '',
                textAreaEmail: '',
                textAreaPhoneNum: '',
                textAreaJoinTime: '',
                textAreaState: '',
                textAreaLostFoundKey: '',
                textAreaUploadCount: '',
                textAreaDownloadCount: '',
                textAreaDivideCount: '',
                demoUserImage: '',
                form3: {
                    password: null,
                    newPassword: null
                },
                form2: {
                    userName: null,
                    email: null,
                    lostFoundKey: null
                },
                form: {
                    userName: null,
                    email: null,
                    password: null
                },
                dialogFormVisible: false,
                dialogForm2Visible: false,
                dialogForm3Visible: false,
                formLabelWidth: '220px',

                signUpAble:false,
                formSignUp: {
                    email: null,
                    userName: null,
                    phoneNumber: null,
                    passWord: null,
                    address1Line1: null,
                    address1Line2: null,
                    address1PostCode: null,
                    address2Line1: null,
                    address2Line2: null,
                    address2PostCode: null,
                    address3Line1: null,
                    address3Line2: null,
                    address3PostCode: null
                },
                yourIp:null,

                //adminView 选择是否需要隐藏（对非 admin隐藏）
                seeState : false,
            };
        },
        methods: {

            //每个界面都有这个，即判断当前登录用户是否是管理员，是的话展示的可操作内容会多i一些
            adminView() {
                if (localStorage.getItem('loginResult') === null) {
                    this.seeState = false;
                }
                else {
                    let currentUserId = JSON.parse(localStorage.getItem('loginResult')).userId;
                    if(currentUserId <= 100 && currentUserId != 2) {
                        this.seeState = true;
                    }
                    else {
                        this.seeState = false;
                    }
                }
            },

            getIp() {

              this.$message({
                showClose: true,
                type: 'warning',
                message: '服务器连接失败,所以有些功能无法使用~'
              });


                fetch('https://api.ipify.org?format=json').then(x => x.json())
                    .then(({ ip }) => {
                        this.yourIp = ip;
                        // this.$message(this.yourIp);
                    });
            },

          takePhoto() {
            this.$message({
              showClose: true,
              message: '很不幸,这个功能还没来得及没写,你可以选择另一种方式~'
            });
          },



            //时间转换函数，后台那串数字解析成可视的时间格式
            getLocalTime(jsondate) {
                jsondate = "" + jsondate + "";//因为jsonDate是number型的indexOf会报错
                if (jsondate.indexOf("+") > 0) {
                    jsondate = jsondate.substring(0, jsondate.indexOf("+"));
                } else if (jsondate.indexOf("-") > 0) {
                    jsondate = jsondate.substring(0, jsondate.indexOf("-"));
                }
                var date = new Date(parseInt(jsondate, 10));
                var month = date.getMonth() + 1 < 10 ? "0" + (date.getMonth() + 1) : date.getMonth() + 1;
                var currentDate = date.getDate() < 10 ? "0" + date.getDate() : date.getDate();
                var hours = date.getHours() < 10 ? "0" + date.getHours() : date.getHours();
                var minutes = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
                var seconds = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();
                return date.getFullYear() + "-" + month + "-" + currentDate + " " + hours + ":" + minutes + ":" + seconds;
            },

            // 界面进来就会根据localStorage存储的当前用户信息，初始化用户详情
            initUserInfo() {
                if (localStorage.getItem('loginResult') === null) {
                    this.initGustLocalStorage();
                } else {
                    this.textAreaUserName = JSON.parse(localStorage.getItem('loginResult')).userName;
                    this.textAreaEmail = JSON.parse(localStorage.getItem('loginResult')).email;
                    this.textAreaPhoneNum = JSON.parse(localStorage.getItem('loginResult')).phoneNumber;
                    this.textAreaJoinTime = this.getLocalTime(JSON.parse(localStorage.getItem('loginResult')).createDate);
                    this.textAreaState = JSON.parse(localStorage.getItem('loginResult')).state;
                    this.textAreaLostFoundKey = JSON.parse(localStorage.getItem('loginResult')).lostFoundKey;
                    this.demoUserImage = JSON.parse(localStorage.getItem('loginResult')).userDetail;
                    this.setAddress();
                }
            },

            setAddress() {
                this.textAreaUploadCount = JSON.parse(localStorage.getItem('loginResult')).address1Line1 + "," +
                    JSON.parse(localStorage.getItem('loginResult')).address1Line2 + "," +
                    JSON.parse(localStorage.getItem('loginResult')).address1PostCode;
                this.textAreaDownloadCount = JSON.parse(localStorage.getItem('loginResult')).address2Line1 + "," +
                    JSON.parse(localStorage.getItem('loginResult')).address2Line2 + "," +
                    JSON.parse(localStorage.getItem('loginResult')).address2PostCode;
                this.textAreaDivideCount = JSON.parse(localStorage.getItem('loginResult')).address3Line1 + "," +
                    JSON.parse(localStorage.getItem('loginResult')).address3Line2 + "," +
                    JSON.parse(localStorage.getItem('loginResult')).address3PostCode;
            },

            //
            // 再请求服务器，得到gust用户的信息
            // 清空localStorage.loginResult；
            // 写入localStorage.loginResult;
            // 再初始化界面的组建为gust的信息
            initGustLocalStorage() {
                this.$http.put("mainView/getUserInfo", {
                    userId: 2 // 1是管理员admin,2是gust
                }).then(result => {
                    var result = result.body;
                    if (result.code === 200) {
                        localStorage.removeItem('loginResult');
                        localStorage.setItem('loginResult', JSON.stringify(result.data))
                        this.textAreaUserName = JSON.parse(localStorage.getItem('loginResult')).userName;
                        this.textAreaEmail = JSON.parse(localStorage.getItem('loginResult')).email;
                        this.textAreaPhoneNum = JSON.parse(localStorage.getItem('loginResult')).phoneNumber;
                        this.textAreaJoinTime = this.getLocalTime(JSON.parse(localStorage.getItem('loginResult')).createDate);
                        this.textAreaState = JSON.parse(localStorage.getItem('loginResult')).state;
                        this.textAreaLostFoundKey = JSON.parse(localStorage.getItem('loginResult')).lostFoundKey;
                        this.demoUserImage = JSON.parse(localStorage.getItem('loginResult')).userDetail;
                        this.setAddress();
                    } else {
                        this.$message('服务器异常');
                    }
                });
            },

            openSignUp() {
                this.signUpAble = true;
            },
            signUp() {
                //检测输入是否合适
                if (!(this.formSignUp.email) || !(this.formSignUp.userName) || !(this.formSignUp.phoneNumber)
                    || !(this.formSignUp.passWord) || !(this.formSignUp.address1Line1)
                    || !(this.formSignUp.address1Line2) || !(this.formSignUp.address1PostCode)) {
                    this.$message('很不幸,这个功能还没来得及没写~');
                    return;
                }
                //后台注册
                this.$http.put("mainView/signUp", {
                    ip: this.yourIp,
                    email: this.formSignUp.email,
                    userName: this.formSignUp.userName,
                    phoneNumber: this.formSignUp.phoneNumber,
                    passWord: this.formSignUp.passWord,
                    address1Line1: this.formSignUp.address1Line1,
                    address1Line2: this.formSignUp.address1Line2,
                    address1PostCode: this.formSignUp.address1PostCode,
                    address2Line1: this.formSignUp.address2Line1,
                    address2Line2: this.formSignUp.address2Line2,
                    address2PostCode: this.formSignUp.address2PostCode,
                    address3Line1: this.formSignUp.address3Line1,
                    address3Line2: this.formSignUp.address3Line2,
                    address3PostCode: this.formSignUp.address3PostCode
                }).then(result => {
                    var result = result.body;
                    if (result.code === 200) {
                        let ret = result.data;
                        let retInfo = ret.retInfo;
                        if(ret.successOrNot == "Y") {
                            this.$message(retInfo);
                            this.form.email = this.formSignUp.email;
                            this.form.password = this.formSignUp.passWord;
                            this.handleSignIn();
                        }
                        else {
                            this.$message(retInfo);
                        }

                    } else {
                        this.$message('失败！');
                    }
                });


            },

            beforeEditProfile() {
                if (2 == JSON.parse(localStorage.getItem('loginResult')).userId) {
                    this.$message('游客身份，尚未登录!!');
                    // alert("");
                    return;
                } else {
                    this.dialogForm3Visible = true;
                }
            },

            editAddress() {
                this.$message("尚不支持！");
            },

            // handleEditProfile
            handleEditProfile() {
                if (!(this.form3.password) || !(this.form3.newPassword)) {
                    this.$message('当前密码或新密码不能为空!');
                    return;
                }
                if (this.form3.password != JSON.parse(localStorage.getItem('loginResult')).passWord) {
                    this.$message('当前密码输入不对!');
                    return;
                }
                this.$http.put("mainView/handleEditProfile", {
                    userId: JSON.parse(localStorage.getItem('loginResult')).userId,
                    newPassWord: this.form3.newPassword
                }).then(result => {
                    var result = result.body;
                    if (result.code === 200) {
                        this.$message('你的密码修改成功，请重新登录！');
                        this.initGustLocalStorage();
                    } else {
                        this.$message('服务器异常');
                    }
                });
            },
            // 检索界面输入，不合法时返回
            // 合法时请求服务器，返回passWord在界面显式
            handleFindUserInfo() {
                if (!(this.form2.userName) && !(this.form2.email) && !(this.form2.lostFoundKey)) {
                    this.$message('请最少填写一项能表明你是谁的信息，不然你是要上天么？');
                    // alert("用户名和邮箱不能同时为空！");
                    return;
                }
              this.$message({
                showClose: true,
                message: '很不幸,这个功能还没来得及没写,你可以选择新注册一个账号~~'
              });


            },
            // 不管当前是什么用户，都可以登陆新用户；
            // 当发现新用户就是本用户时，提示无需登陆
            // 当登录gust用户时，提示登出即可
            handleSignIn() {
                if (!(this.form.userName) && !(this.form.email)) {
                    alert("用户名和邮箱不能同时为空！");
                    return;
                }
                if (!(this.form.password)) {
                    alert("password 不能为空!");
                    return;
                }
                if (this.form.userName == 'gust') {
                    alert("gust用户无需登录!");
                    return;
                }
                this.$http.put("mainView/getUserInfo", {
                    userName: this.form.userName,
                    email: this.form.email,
                    passWord: this.form.password
                }).then(result => {
                    var result = result.body;
                    if (result.code === 200) {
                        localStorage.removeItem('loginResult');
                        localStorage.setItem('loginResult', JSON.stringify(result.data))
                        this.textAreaUserName = JSON.parse(localStorage.getItem('loginResult')).userName;
                        this.textAreaEmail = JSON.parse(localStorage.getItem('loginResult')).email;
                        this.textAreaPhoneNum = JSON.parse(localStorage.getItem('loginResult')).phoneNumber;
                        this.textAreaJoinTime = this.getLocalTime(JSON.parse(localStorage.getItem('loginResult')).createDate);
                        this.textAreaState = JSON.parse(localStorage.getItem('loginResult')).state;
                        this.textAreaLostFoundKey = JSON.parse(localStorage.getItem('loginResult')).lostFoundKey;
                        this.demoUserImage = JSON.parse(localStorage.getItem('loginResult')).userDetail;
                        this.setAddress();
                        //刷新当前页面
                        window.location.reload();
                        alert("登入成功");
                    } else if (result.code === 499) {
                        alert(result.data.handleSignInErrRet);
                    } else {
                        this.$message('服务器异常');
                    }
                });
            },
            // 登出操作.先判断localStorage，如果为gust,提示无需登出;否则清空localStorage,然后将gust信息导入.
            handleSignOut() {
                if (JSON.parse(localStorage.getItem('loginResult')).userId == 2) {
                    alert("gust用户无需登出");
                }
                else {
                    this.$http.put("mainView/getUserInfo", {
                        userId: 2 // 1是管理员admin,2是gust
                    }).then(result => {
                        var result = result.body;
                        if (result.code === 200) {
                            localStorage.removeItem('loginResult');
                            localStorage.setItem('loginResult', JSON.stringify(result.data))
                            this.textAreaUserName = JSON.parse(localStorage.getItem('loginResult')).userName;
                            this.textAreaEmail = JSON.parse(localStorage.getItem('loginResult')).email;
                            this.textAreaPhoneNum = JSON.parse(localStorage.getItem('loginResult')).phoneNumber;
                            this.textAreaJoinTime = this.getLocalTime(JSON.parse(localStorage.getItem('loginResult')).createDate);
                            this.textAreaState = JSON.parse(localStorage.getItem('loginResult')).state;
                            this.textAreaLostFoundKey = JSON.parse(localStorage.getItem('loginResult')).lostFoundKey;
                            this.demoUserImage = JSON.parse(localStorage.getItem('loginResult')).userDetail;
                            this.setAddress();
                            //刷新当前页面
                            window.location.reload();
                            alert("登出成功，现在是gust身份");
                        } else {
                            this.$message('服务器异常');
                        }
                    });
                }
            }
        }
    };
</script>