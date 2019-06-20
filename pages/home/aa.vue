<template>
    <view class="content">
        <!-- <image class="logo" src="../../static/logo.png"></image> -->
        <view class="titletal">
            <text class="title">{{ title }}</text>
        </view>
        <from name="from1">
            <!--账号-->
            <view class="inputView">
                <image class="nameImage" src="../../static/name.png"></image>
                <label class="loginLab">账号</label>
                <input
                    class="inputText"
                    type="text"
                    placeholder="请输入账号"
                    value="user"
                    v-model="uname"
                />
            </view>
        </from>
        <view class="line"></view>
        <!--密码-->
        <view class="inputView">
            <image class="keyImage" src="../../static/key.png"></image>
            <label class="loginLab">密码</label>
            <input
                class="inputText"
                password="true"
                type="text"
                placeholder="请输入密码"
                value="pass"
                v-model="passw"
            />
        </view>
        <!-- 记住密码 -->
        <view class=" mui-input-row mui-checkbox ">
            <!-- <input id="chkRem" type="checkbox" checked="checked" class="RememberCheck"  @change="checkboxChange" /> -->
            <checkbox-group @change="checkboxChange">
                <checkbox
                    id="chkRem"
                    type="checkbox"
                    :checked="rememberPsw"
                    @tap="rememberPsw = !rememberPsw"
                    class="RememberCheck"
                >
                    记住密码
                </checkbox>
                <!-- <lable for="chkRem" class="RememberPass">记住密码</lable> -->
            </checkbox-group>
        </view>

        <!--按钮-->
        <view class="loginBtnView"><button class="loginBtn" @tap="lands">登录</button></view>

 <!--背景图-->      

<!--  <image class="backlogo" src="../../static/BGNew.png"></image>-->
    </view>
</template>

<script>
var self;

var webapiaddress = null; //链接地址
export default {
    data() {
        lists: [], (self = this);
        return {
            title: '标题',
            uname: '',
            passw: '',
            rememberPsw: true
        };
    },
    //页面初始加载
    mounted() {
        let that = this;

        //缓存的账号
        const HCuname = uni.getStorageSync('HCuname');
        //缓存的密码
        const HCpassw = uni.getStorageSync('HCpassw');
        //         console.log(HCpassw+"缓存的密码")
        //         console.log(HCuname)
        //有缓存就赋值给文本没有就清空
        if (HCuname && HCpassw) {
            that.uname = HCuname;
            that.passw = HCpassw;
        } else {
            that.uname = '';
            that.passw = '';
        }
    },
    methods: {
        //             //用户名：
        //         nameChange:function(e){
        //             this.uname=e.traget.value
        //         },
        //         //密码：
        //         passChange:function(e){
        //             this.passw=e.traget.value
        //         },

        //登陆
        lands() {
            if (this.uname.length <= 0 || this.passw.length <= 0) {
                uni.showToast({
                    title: '账号或密码不能为空',
                    icon: 'none'
                });
                return;
            } else {
                let TFTwoName = this.uname.substring(0, 2);
                let TFLastName = this.uname.substring(2);
                let Passwd = this.passw;
          

                var that = this;
                //链接登录  （我这是两次，第一次获取链接地址，第二次才为登录 ）
                uni.request({
                    url: 'http链接地址',
                    success: res => {
                        var sabb = [];
                    
                        // console.log(webapiaddress+"链接地址")
                        //打印链接地址
                       

                       //这里是登录（你可以直接在这里进行操作你的登录链接上面的你要删除包含对应的括号）
                        var that = this;
                        uni.request({
                            url: '' + webapiaddress + '/api/User', //链接地址
                            data: {
                                strUser: TFLastName,
                                strPwd: Passwd
                            },
                            dataType: 'json',
                            success: res => {
                                //成功
                                if (res.data.IsSuccess == true) {
                                    
                                    //缓存账号和密码
                                    if (that.rememberPsw) {
                                        uni.setStorageSync('HCuname', that.uname);
                                        uni.setStorageSync('HCpassw', that.passw);
                                    } else {
                                        uni.removeStorageSync('HCuname');
                                        uni.removeStorageSync('HCpassw');
//                                         that.uname = '';
//                                         that.passw = '';
                                    }
                                    uni.navigateTo({
                                        url: '../index/index'
                                    });
                                } else {
                                    uni.showToast({
                                        title: '用户名或密码错误',
                                        icon: 'none'
                                    });
                                }
                            }
                        });
                    }
                });
            }
        },

        //复选框
        checkboxChange: function(e) {
        
            console.log(e.detail.value.length);
            if (e.detail.value.length == 1) {
    
                //获取缓存的账号
                 uni.getStorageSync('HCuname',this.uname);
                 uni.getStorageSync('HCpassw',this.passw);
            } else {
                  uni.removeStorageSync('HCuname');
                  uni.removeStorageSync('HCpassw');              
            }
        }
    }
};
</script>

<style>
.mui-checkbox input[type='checkbox']:checked:before {
    color: #00bbb1;
}
.RememberPass {
    color: #adadad;

    margin-top: 5px;
}
.RememberCheck {
    margin-left: -50%;
    margin-top: 10px;
    color: #adadad;
}
.content {
    text-align: center;
    height: 400upx;
}
.backlogo {
    padding-bottom: 0px;
    position: absolute;
    bottom: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
    z-index: -1;
}
.logo {
    height: 200upx;
    width: 200upx;
    margin-top: 200upx;
}
.titletal {
    margin-top: 90upx;
    height: 75px;
}
.title {
    /* font-size: 36upx; */
    color: mediumaquamarine;
    font-size: 150%;
}

.text {
    border: 1, solid, black;
}

.login-from {
    /* margin-top: 30%; */

    flex: auto;
    height: 100%;
    width: 100%;
}

.inputView {
    background-color: #fff;
    line-height: 50px;
    border-width: 1px;
    border-bottom: 2dp;
}

/*输入框*/
.nameImage,
.keyImage {
    margin-left: 22px;
    width: 18px;
    height: 18px;
}

.loginLab {
    margin: 15px 15px 15px 10px;
    color: #545454;
    font-size: 18px;
}

.inputText {
    flex: block;
    float: right;
    text-align: left;
    margin-right: 22px;
    margin-top: 15px;
    color: #000000;
    font-size: 18px;
}

.line {
    width: 100%;
    height: 1px;
    background-color: #cccccc;
    margin-top: 1px;
}

/*按钮*/
.loginBtnView {
    width: 100%;
    height: auto;
    /* background-color:#FFFFFF; */
    margin-top: 20px;
    margin-bottom: 0px;
    padding-bottom: 0px;
}

.loginBtn {
    width: 80%;
    margin-top: 50px;
    background-color: mediumaquamarine;
    color: aliceblue;
}
</style>
