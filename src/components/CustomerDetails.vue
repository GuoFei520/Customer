<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
      {{customer.name}}
      <span class="pull-right">
        <router-link v-bind:to="'/edit/' + customer.id" class="btn btn-primary">编辑</router-link>
        <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item">
        <i class="iconfont icon-weibiaoti"></i>&nbsp;{{customer.phone}}
      </li>
      <li class="list-group-item">
        <i class="iconfont icon-youxiang"></i>&nbsp;{{customer.email}}
      </li>
    </ul>
    <ul class="list-group">
      <li class="list-group-item">
        <i class="iconfont icon-xueli"></i>&nbsp;{{customer.education}}
      </li>
      <li class="list-group-item">
        <i class="iconfont icon-daxue"></i>&nbsp;{{customer.graduationschool}}
      </li>
      <li class="list-group-item">
        <i class="iconfont icon-gongzuo"></i>&nbsp;{{customer.profession}}
      </li>
      <li class="list-group-item">
        <i class="iconfont icon-jianjie"></i>&nbsp;{{customer.profile}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "customerdetails",
  data() {
    return {
      customer: ""
    };
  },
  methods: {
    fetchCustomers(id) {
      this.$http.get("http://localhost:3004/users/" + id).then(response => {
        this.customer = response.data;
      });
    },
    deleteCustomer(id) {
      // console.log(id);
      this.$http.delete("http://localhost:3004/users/" + id).then(response => {
        this.$router.push({ path: "/", query: { alert: "用户删除成功!" } });
      });
    }
  },
  created() {
    this.fetchCustomers(this.$route.params.id);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
