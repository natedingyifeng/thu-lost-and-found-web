<template>
  <div>
    <el-card class='card'
             style="margin-top:20px;">
      <h2 style="text-align:center;">
        紫荆寻物THU网页端使用指南
      </h2>
      <p style="text-indent:2em;">
        紫荆寻物THU是面向清华师生的一款失物招领&寻物启事发布平台，致力于为清华师生提供一个更好的寻物平台。紫荆寻物THU拥有网页端和小程序端两个界面，其中小程序面向的是普通用户，而网页端面向的是管理员。本使用指南将指导平台管理者使用紫荆寻物THU网页端对平台进行管理。
      </p>
      <h3 style="text-align:left;">
        使用人群
      </h3>
      <p style="text-indent:2em;">
        本网站面向紫荆寻物THU平台管理员，包括平台维护人员、教室管理员、宿舍管理员、校团委老师等可能会参与到平台的日常管理的管理人员。
      </p>
      <h3 style="text-align:left;">
        寻物启事/失物招领列表
      </h3>
      <p style="text-indent:2em;">
        在这两个启事列表里，你可以看到所有列举在表格里的简略的启事信息，包括启事ID、创建时间、创建者、物品、地点、时间、状态等信息。表格上方是搜索和筛选框，在里面选择与输入就可以对启事信息进行搜索与筛选。表格右上方有“新建寻物启事/失物招领”按钮，管理员可以点击此按钮发布新的寻物启事/失物招领。
      </p>
      <h3 style="text-align:left;">
        寻物启事/失物招领详情
      </h3>
      <p style="text-indent:2em;">
        点击启事列表里的表项，即可进入启事详情页。在启事详情页，你可以看到启事的所有详情信息，包括启事的基本信息、启事的图片、地点、与该启事相匹配的失物招领/寻物启事等信息。点击启事右上方的“修改”按钮，管理员可以对每一个启事进行修改；点击“确定”按钮，后端就会处理启事的修改请求并反馈；点击“删除”按钮，管理员可以将该启事删除。启事正下方为该启事的匹配信息，其中详细列举了与该启事有关的启事和它们的匹配度。点击对应的链接即可查看对应的启事。
      </p>
      <h3 style="text-align:left;">
        用户列表与用户详情
      </h3>
      <p style="text-indent:2em;">
        在用户列表里，管理员可以看到用户的一些信息，包括用户的姓名、用户名、联系方式、状态等等。点击用户列表的表项，可以进入用户的详情页。在用户详情页，你可以看到用户的所有基本信息，包括登录时间、联系方式、头像等等。分别点击右上方的“修改”、“确定”和“删除”按钮，即可对用户信息进行对应的操作（与启事类似）；点击右上方的“封禁”按钮，可以将该用户封禁。用户信息的正下方用时间轴的方式展示了该用户所有发布过的启事，点击相应的链接即可查看对应的启事信息。
      </p>
      <h3 style="text-align:left;">
        认证申请/举报处理
      </h3>
      <p style="text-indent:2em;">
        在认证申请里，管理员可以看到所有用户提交的需要管理员手动确认的认证申请，点进详情页后，点击右上方的“通过”或“否决”按钮来决定是否通过对应的认证申请。如果认证申请通过，提交该申请的用户则会自动成为认证用户。在举报处理里，管理员可以看到所有用户提交的举报信息，点进详情页后，点击右上方的“通过”或“否决”按钮来决定是否通过对应的举报。如果管理员决定通过这一举报，那么管理员需要同时填写一个理由，作为该举报里被举报用户的封禁理由。
      </p>
      <h3 style="text-align:left;">
        物品列表/物品详情
      </h3>
      <p style="text-indent:2em;">
        在物品列表里，管理员可以对创建启事时需要选择的物品种类和物品模板进行添加、编辑和删除，其中对物品种类的添加、编辑和删除都是在物品列表页进行的，而物品模板的添加、编辑和删除则可以到物品模板的详情页进行处理，其基本操作与启事类似。
      </p>
      <h3 style="text-align:left;">
        创建账号
      </h3>
      <p style="text-indent:2em;">
        在创建账号里，管理员可以选择两种方式创建新的账号：第一，向需要创建账号的管理者发送一封邮件，然后让其填写相关信息进行注册；第二，管理员直接在页面里填写必要的注册信息，然后创建用户。
      </p>
      <h3 style="text-align:left;">
        启事匹配
      </h3>
      <p style="text-indent:2em;">
        在启事匹配里，管理者可以看到所有启事之间的匹配的情况，包括启事简要信息、匹配度、匹配状态等等。管理员可以在页面上手动点击“通知”按钮，将对应的匹配信息发送给对应的用户。点击表格右上方的“修改匹配参数”，管理员可以对匹配算法里的一些参数进行修改。
      </p>
      <h3 style="text-align:left;">
        平台信息
      </h3>
      <p style="text-indent:2em;">
        在平台信息里，管理者可以看到两部分数据统计：用户数据和启事数据。在用户数据里，管理员可以看到不同状态和不同身份的用户的人数以及在全体用户里的比重。在启事数据里，管理员可以看到失物招领和寻物启事的数量和成功率，并且可以以折线图的形式看到启事在不同时间段的发送情况。
      </p>
    </el-card>
    <div>
    </div>
  </div>
</template>

<style scoped>
.el-card {
  margin-right: 15%;
  margin-left: 15%;
  margin-bottom: 5%;
}
</style>

<script>
/* eslint-disable @typescript-eslint/camelcase */

import Axios from 'axios'
export default {
  props: {
    token: String
  },
  data: function () {
    return {

    }
  },
  created: function () {
    
  },
  methods: {
    
  }
}
</script>
