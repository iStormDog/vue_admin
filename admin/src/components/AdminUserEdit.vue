<template>
    <div>
        <h1>{{id?'编辑':'新建'}}管理员</h1>
        <el-form @submit.native.prevent="save">
            <el-form-item label="用户名" label-width="80px">
                <el-input v-model="model.username"></el-input>
            </el-form-item>
            <el-form-item label="密码" label-width="80px">
                <el-input type="text" v-model="model.password"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" native-type="submit">保存更改</el-button>
            </el-form-item>
        </el-form>
    </div>    
</template>
<script>
/* eslint-disable */
export default {
    props:{
        id:{}
    },
    data(){
        return {
            model:{
                username:'',
                password:''
            },
        }
    },
    methods:{
        async save(){        
            let res    
            if(this.id){
                const res=await this.$http.put('rest/admin_users/'+this.id,this.model);
            }
            else{
                const res=await this.$http.post('rest/admin_users',this.model);
            }
            
            this.$message({
                type:'success',
                message:'保存成功'
            })
            this.$router.push('/admin_users/list')
        },
        async fetch(){
            const res=await this.$http.get(`rest/admin_users/${this.id}`);
            this.model=res.data;
        },
    },
    created(){
        this.id && this.fetch()
    },
}
</script>