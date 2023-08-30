<template>
  <div id="UserLoginView">
    <h2 style="margin-bottom: 16px">&nbsp;&nbsp;用户注册</h2>
    <a-form
      :model="form"
      style="max-width: 300px; margin: 0 auto"
      label-align="left"
      auto-label-width
      @submit="handleSubmit"
    >
      <a-form-item field="userAccount" tooltip="账号4位以上" label="账号">
        <a-input v-model="form.userAccount" placeholder="请输入账号" />
      </a-form-item>
      <a-form-item field="userPassword" tooltip="密码8位以上" label="密码">
        <a-input-password
          v-model="form.userPassword"
          placeholder="请输入密码"
        />
      </a-form-item>
      <a-form-item field="checkPassword" tooltip="密码8位以上" label="密码">
        <a-input-password
          v-model="form.checkPassword"
          placeholder="请再次输入密码"
        />
      </a-form-item>
      <a-form-item>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a-button
          style="width: 120px"
          html-type="submit"
          type="primary"
          >注册
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script setup lang="ts">
import { reactive } from "vue";
import { UserControllerService, UserRegisterRequest } from "../../../generated";
import message from "@arco-design/web-vue/es/message";
import { useRouter } from "vue-router";
const form = reactive({
  userAccount: "",
  userPassword: "",
  checkPassword: "",
} as UserRegisterRequest);

const router = useRouter();
/**
 * 提交表单
 * @param
 */
const handleSubmit = async () => {
  const res = await UserControllerService.userRegisterUsingPost(form);
  //注册成功，跳转登录页面
  if (res.code == 0) {
    router.push({
      path: "/user/login",
      replace: true,
    });
  } else {
    message.error("注册失败");
  }
};
</script>
