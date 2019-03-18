<!--<template>-->
    <!--<div>-->
        <!--<form action="" v-if="!isReg">-->
            <!--<div>用户名：</div>-->
            <!--<input type="text" v-model="name">-->
            <!--<div>密码：</div>-->
            <!--<input type="password" v-model="password">-->
            <!--<div>-->
            <!--<button type="button" @click="login()">登陆</button>-->
            <!--<button type="button" @click="reg()">注册</button>-->
            <!--</div>-->
        <!--</form>-->
        <!--<form action="" v-else>-->
            <!--<div>用户名：</div>-->
            <!--<input type="text" v-model="name">-->
            <!--<div>密码：</div>-->
            <!--<input type="password" v-model="password">-->
            <!--<div>再次输入密码：</div>-->
            <!--<input type="password" v-model="repeat">-->
            <!--<div>-->
            <!--<button type="button" @click="addUser()">确定</button>-->
            <!--<button type="button" @click="cancel()">取消</button>-->
            <!--</div>-->
        <!--</form>-->
    <!--</div>-->
<!--</template>-->
<template>
    <div>
    <Form ref="formInline" :model="formInline" :rules="ruleInline" v-if="!isReg" inline>
        <FormItem prop="name">
            <Input type="text" v-model="formInline.name" placeholder="Name">
                <Icon type="ios-person-outline" slot="prepend"></Icon>
            </Input>
        </FormItem>
        <FormItem prop="password">
            <Input type="password" v-model="formInline.password" placeholder="Password">
                <Icon type="ios-lock-outline" slot="prepend"></Icon>
            </Input>
        </FormItem>
        <FormItem>
            <Button type="primary" @click="login()">登陆</Button>
        </FormItem>
        <FormItem>
            <Button type="primary" @click="reg()">注册</Button>
        </FormItem>
    </Form>
        <Form ref="formInline" :model="formInline" :rules="ruleInline" v-else inline>
            <FormItem prop="name">
                <Input type="text" v-model="formInline.name" placeholder="Name">
                    <Icon type="ios-person-outline" slot="prepend"></Icon>
                </Input>
            </FormItem>
            <FormItem prop="password">
                <Input type="password" v-model="formInline.password" placeholder="Password">
                    <Icon type="ios-lock-outline" slot="prepend"></Icon>
                </Input>
            </FormItem>
            <FormItem prop="password">
                <Input type="password" v-model="formInline.repeat" placeholder="Comfirm Password">
                    <Icon type="ios-lock-outline" slot="prepend"></Icon>
                </Input>
            </FormItem>
            <FormItem>
                <Button type="primary" @click="addUser()">确定</Button>
            </FormItem>
            <FormItem>
                <Button type="primary" @click="cancel()">取消</Button>
            </FormItem>
        </Form>
    </div>
</template>

<script>
    export default {
        name: "Login",
        data() {
            return {
                isReg: false,
                formInline: {
                    name: '',
                    password: '',
                    repeat: ''
                },
                ruleInline: {
                    name: [
                        {required: true, message: '用户名不能为空', trigger: 'blur'}
                    ],
                    password: [
                        {required: true, message: '密码不能为空.', trigger: 'blur'},
                        {
                            type: 'string',
                            min: 3,
                            message: '密码不能少于三个字符',
                            trigger: 'blur'
                        }
                    ]
                }
            }
        },
        methods:{
            login() {
                if(localStorage.getItem("name") == this.formInline.name && localStorage.getItem("password") == this.formInline.password){
                    this.formInline.name = ''
                    this.formInline.password = ''
                    this.$router.push('/home/list')
                }else{
                    alert('用户名密码不正确')
                }
            },
            reg(){
                this.isReg = true
                this.formInline.name = ''
                this.formInline.password = ''
            },
            addUser() {
                if(this.formInline.password == this.formInline.repeat) {
                    localStorage.setItem("name", this.formInline.name)
                    localStorage.setItem("password", this.formInline.password)
                    this.formInline.name = ''
                    this.formInline.password = ''
                    this.isReg = false
                } else{
                    alert('两次密码输入不一致')
                }
            },
            cancel() {
                this.isReg = false
            }
        }
    }
</script>

<style scoped>

</style>
