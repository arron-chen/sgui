<template>
  <div class="module-page">
    <div class="title">
      <div class="back" onclick="window.history.go(-1)">返回</div>
      <p class="name">印章</p>
    </div>
    <div class="wrap">
      <el-collapse v-model="activeNames" @change="handleChange">
        <el-collapse-item title="组件演示" name="1">
          <div class="mt-25">
            <label class="left-label">基础用法:</label>
            <seal></seal>
          </div>
          <div class="mt-25">
            <label class="left-label">自定义宽高:</label>
            <seal iWidth="50" iHeight="50"></seal>
          </div>
          <div class="mt-25">
            <label class="left-label">自定义内容:</label>
            <seal name="测试章xx" organization="广东省国土资源部"></seal>
          </div>
        </el-collapse-item>
        <el-collapse-item title="使用说明" name="2">
          示例代码：
          <div class="code">
            基础用法： {{code1}}

          </div>
          <div class="code">
            自定义宽高：  {{code2}}
          </div>
          <div class="code">
            自定义内容：  {{code3}}
          </div>
        </el-collapse-item>
        <el-collapse-item title="API" name="3">
          <table>
            <thead>
            <th>属性</th>
            <th>说明</th>
            <th>类型</th>
            <th>默认值</th>
            </thead>
            <tbody>
            <tr>
              <td>iWidth</td>
              <td>印章宽度</td>
              <td>Number</td>
              <td>250</td>
            </tr>
            <tr>
              <td>iHeight</td>
              <td>印章高度</td>
              <td>String</td>
              <td>250</td>
            </tr>
            <tr>
              <td>name</td>
              <td>图片印章名称</td>
              <td>String</td>
              <td>测试专用章</td>
            </tr>
            <tr>
              <td>organization</td>
              <td>图片印章单位名称</td>
              <td>String</td>
              <td>南方数码研发中心团队</td>
            </tr>
            </tbody>
          </table>
        </el-collapse-item>
      </el-collapse>
    </div>
  </div>
</template>
<script>
  import seal from '../../components/signet.vue'
  export default {
    data(){
      return{
        activeNames:['1','2','3'],
        code1:`<seal></seal>`,
        code2:`<seal iWidth="50" iHeight="50"></seal>`,
        code3:`<seal name="测试章xx" organization="广东省国土资源部"></seal>`
      }
    },
    components:{seal},
    methods:{
      handleChange(val){
        console.log(val);
      },
    },
  }
</script>
<style>
  .mt-25{
    margin-top:25px;
  }
  .mb-20{
    margin-bottom:20px;
  }
  .left-label{
    padding:0 10px;
    width:80px;
    display: inline-block;
  }
  table{
    font-family: Consolas,Menlo,Courier,monospace;
    font-size: 12px;
    border-collapse: collapse;
    border-spacing: 0;
    empty-cells: show;
    border: 1px solid #e9e9e9;
    width: 100%;
    margin-bottom: 24px;
  }
  table th {
    border: 1px solid #e9e9e9;
    padding: 8px 16px;
    text-align: left;
    background: #f7f7f7;
    white-space: nowrap;
    color: #5c6b77;
    font-weight: 600;
  }
  table td, table th {
    border: 1px solid #e9e9e9;
    padding: 8px 16px;
    text-align: left;
  }
  .code{
    border-radius: 3px;
    background-color:#f7f7f7;
    color: inherit;
    padding:5px 10px;

  }
</style>
