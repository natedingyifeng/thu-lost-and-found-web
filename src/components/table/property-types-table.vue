<template>
  <div>
    <el-card class="title-card">
      所有物品
      <div class="edit">
        <el-button :id="id"
                    target="rent-application"
                    class="change"
                    @click="type_dialogFormVisible = true"
                    type="primary">新建物品种类</el-button>
        <el-button :id="id"
                    target="rent-application"
                    class="change"
                    @click="template_dialogFormVisible = true"
                    type="primary">新建物品模板</el-button>
      </div>
    </el-card>
    <el-dialog class="create_contact" title="添加属性" :visible.sync="create_field_dialogFormVisible">
      <el-form label-width="100px">
        <el-form-item label="属性名称">
          <el-input autocomplete="off" v-model="create_field.name"></el-input>
        </el-form-item>
        <el-form-item label="属性权重">
          <el-input-number v-model="create_field.details" controls-position="right" :min="1" :max="10" size="mini" width="60%"></el-input-number>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <div class="foot">
          <el-button @click="create_field_dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="createField">确 定</el-button>
        </div>
      </div>
    </el-dialog>
    <el-dialog class="edit_contact" title="修改属性" :visible.sync="edit_field_dialogFormVisible">
      <el-form label-width="100px">
        <el-form-item label="属性名称">
          <el-input autocomplete="off" v-model="edit_field.name"></el-input>
        </el-form-item>
        <el-form-item label="属性名称">
          <el-input-number v-model="edit_field.details" controls-position="right" :min="1" :max="10" size="mini" width="60%"></el-input-number>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <div class="foot">
          <el-button @click="edit_field_dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="editField">确 定</el-button>
        </div>
      </div>
    </el-dialog>
    <el-dialog class="new_type" title="新建物品种类" :visible.sync="type_dialogFormVisible">
      <el-form label-width="100px">
        <el-form-item label="物品种类名称">
          <el-input autocomplete="off" v-model="type_name.name"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <div class="foot">
          <el-button @click="type_dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="CreateNewType">确 定</el-button>
        </div>
      </div>
    </el-dialog>
    <el-dialog class="edit_type" title="修改物品种类" :visible.sync="type_edit_dialogFormVisible">
      <el-form label-width="100px">
        <el-form-item label="物品种类名称">
          <el-input autocomplete="off" v-model="type_name.name"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <div class="foot">
          <el-button @click="type_dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="EditType">确 定</el-button>
        </div>
      </div>
    </el-dialog>
    <el-dialog class="new_type" title="新建物品模板" :visible.sync="template_dialogFormVisible">
      <el-form label-width="100px">
        <el-divider>基本信息</el-divider>
        <el-form-item label="物品模板名称">
          <el-input autocomplete="off" v-model="template.name"></el-input>
        </el-form-item>
        <el-form-item label='物品种类'
                      class="label">
          <el-select v-model="template.type">
            <el-option v-for="item in property_type_list.results"
                      :key="item.id"
                      :label="item.name"
                      :value="item.id">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label='模板图片'>
          <el-upload
            class="avatar-uploader"
            action="none"
            :on-preview="handleImageUploadSuccess"
            list-type="picture-card"
            :auto-upload="false"
            :on-change="checkType"
            :limit="1"
            :on-exceed="handleExceed">
            <i v-if="!image_visible" class="el-icon-plus"></i>
          </el-upload>
          <el-dialog :visible.sync="image_visible">
            <img width="100%" :src="template.thumbnail_url" alt="">
          </el-dialog>
        </el-form-item>
        <el-divider>模板属性</el-divider>
        <el-form-item label=''
                      class="label"
                      label-width="40px">
          <el-table
            :data="template_fields"
            style="width: 100%">
            <el-table-column
              prop="name"
              label="名称"
              width="330">
            </el-table-column>
            <el-table-column
              prop="details"
              label="权重"
              width="330">
            </el-table-column>
            <el-table-column>
              <template slot="header" slot-scope="scope">
                操作
                <el-button
                  size="mini"
                  type="primary"
                  icon="el-icon-plus"
                  @click="handleFieldCreate(scope.$index, scope.row)"
                  circle></el-button>
              </template>
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  @click="handleFieldEdit(scope.$index, scope.row)">编辑</el-button>
                <el-button
                  size="mini"
                  type="danger"
                  @click="handleFieldDelete(scope.$index, scope.row)">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <div class="foot">
          <el-button @click="template_dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="CreateNewTemplate">确 定</el-button>
        </div>
      </div>
    </el-dialog>
    <search-filter :options="options"
                   @search="searchAndFilter"></search-filter>
    <el-card class="table-card">
      <el-table :data="property_type_list.results"
                id="users-table"
                class="table"
                @row-click="enter"
                row-key="name"
                :tree-props="{children: 'templates'}"
                @sort-change='sortChange'>
        <el-table-column prop="id"
                         sortable='custom'
                         label="ID"
                         width="100">
        </el-table-column>
        <el-table-column prop="name"
                         sortable='custom'
                         label="名称"
                         width="1000">
        </el-table-column>
        <el-table-column label="操作"
                         width="200">
          <template slot-scope="scope">
            <el-button
              size="mini"
              type="danger"
              @click.native.stop="handleDelete(scope.$index, scope.row)">删除</el-button>
            <el-button
              v-if="!(scope.row.type)"
              size="mini"
              @click.native.stop="handleEdit(scope.$index, scope.row)">编辑</el-button>
          </template>
        </el-table-column>
      </el-table>
      <el-pagination
        background
        layout="prev, pager, next"
        :total="types_sum"
        class="page-chooser"
        @current-change="changePage"
        v-if="pagination_update">
      </el-pagination>
    </el-card>
  </div>
</template>

<style scoped>
.title-card {
  margin: auto;
  margin-top: 20px;
  position: relative;
  width: 1350px;
}
.table {
  position: relative;
  margin: 0 auto 40px auto;
  width: 1350px;
}
.table-card{
  position: relative;
  margin: 0 auto 0 auto;
  width: 1350px;
}
.page-chooser {
  position: relative;
  left: 43%;
  top: -10px;
}
.edit{
  position: relative;
  float: right;
  margin: auto;
  margin-bottom: 20px;
}
.foot{
  position: relative;
  top: -20px;
}
</style>

<script>
import Axios from 'axios'
import searchAndFilter from '../search&filter'
export default {
  components: {
    'search-filter': searchAndFilter
  },
  props: {
    id: Number,
    pageSize: Number,
    height: Number
  },
  data: function () {
    return {
      type_dialogFormVisible: false,
      type_edit_dialogFormVisible: false,
      template_dialogFormVisible: false,
      image_visible: false,
      type_edit_id: -1,
      property_template_list: [],
      property_type_list: [],
      options: [
        { value: 'search', label: '全部搜索' },
        { value: 'name', label: '筛选：名称' }
      ],
      select: 'search',
      input: '',
      type_name: {
        name: ''
      },
      template: {
        name: '',
        type: '',
        thumbnail: null,
        thumbnail_url: '',
        fields: ''
      },
      template_fields: [],
      inputVisible: false,
      inputValue: '',
      data: { count: 0 },
      create_field_dialogFormVisible: false,
      edit_field_dialogFormVisible: false,
      edit_field_id: -1,
      field_show: [],
      edit_field: {
        name: "",
        details: ""
      },
      create_field: {
        name: "",
        details: ""
      },
      types_sum: 0,
      pages_sum: 0,
      pagination_update: true
    }
  },
  created: function () {
    Axios.get('/property-types', {})
      .then((response) => {
          this.property_type_list = response.data
          this.types_sum = response.data.count
          this.pagination_update = false
          this.$nextTick(() => {
            this.pagination_update = true
          })
      })
      .catch((error) => {
        alert('error:' + error)
      })
    // this.changePage(1)
  },
  methods: {
    createField() {
      let tem = JSON.parse(JSON.stringify(this.create_field))
      this.template_fields.push(tem)
      this.create_field.name = ""
      this.create_field.details = ""
      this.create_field_dialogFormVisible = false
    },
    editField() {
      let tem = JSON.parse(JSON.stringify(this.edit_field))
      this.$set(this.template_fields, this.edit_field_id, tem)
      this.edit_field.name = ""
      this.edit_field.details = ""
      this.edit_field_dialogFormVisible = false
    },
    handleFieldEdit(index, row) {
      this.edit_field_dialogFormVisible = true
      this.edit_field_id = index
    },
    handleFieldCreate(index, row) {
      this.create_field_dialogFormVisible = true
    },
    handleFieldDelete(index, row) {
      this.template_fields.splice(index, 1)
    },
    handleClose(item) {
      this.template_fields.splice(this.template_fields.indexOf(item), 1);
    },
    showInput() {
      this.inputVisible = true;
      this.$nextTick(_ => {
        this.$refs.saveTagInput.$refs.input.focus();
      });
    },
    handleInputConfirm() {
      let inputValue = this.inputValue;
      if (inputValue) {
        this.template_fields.push({name:inputValue})
      }
      this.inputVisible = false;
      this.inputValue = '';
    },
    sortChange: function(column, prop, order) {
      let order_prop
      if(column.order == "descending")
      {
        order_prop = "-" + column.prop
      }
      else
      {
        order_prop=column.prop
      }
      Axios.get('/property-types/', {
        params: {
          ordering: order_prop,
        }
      })
        .then((response) => {
          this.property_type_list = response.data
        }).catch((error) => {
          this.$alert(error.response.data)
        })
    },
    handleEdit(index, row) {
      this.type_edit_dialogFormVisible = true
      this.type_edit_id = row.id
    },
    EditType() {
      const data = {
        name: this.type_name.name
      }
      Axios({
        url: '/property-types/'+this.type_edit_id+'/',
        method: 'put',
        data: data,
        headers: {
          Authorization: 'Bearer ' + this.$store.getters.getUserAccessToken
        }
      })
        .then((response) => {
          this.type_edit_dialogFormVisible = false
          this.reload()
        })
        .catch((error) => {
          alert('error:' + error)
        })
      this.type_edit_dialogFormVisible = false
    },
    handleDelete(index, row) {
      if(row.type)
      {
        this.DeleteTemplateConfirm(row.id)
      }
      else
      {
        this.DeleteTypeConfirm(row.id)
      }
    },
    DeleteTypeConfirm(id) {
      this.$confirm('此操作将删除该物品种类, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.DeleteType(id)
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      return false
    },
    DeleteType(id){
      Axios.delete('/property-types/' + id + '/', {
        headers: {
          Authorization: 'Bearer ' + this.$store.getters.getUserAccessToken
        }
      })
        .then((response) => {
            this.reload()
        })
        .catch((error) => {
          alert('error:' + error)
        })
      this.$message({
        type: 'success',
        message: '删除成功!'
      });
    },
    DeleteTemplateConfirm(id) {
      this.$confirm('此操作将删除该物品模板, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.DeleteTemplate(id)
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      return false
    },
    DeleteTemplate(id){
      Axios.delete('/property-templates/' + id + '/', {
        headers: {
          Authorization: 'Bearer ' + this.$store.getters.getUserAccessToken
        }
      })
        .then((response) => {
            this.reload()
        })
        .catch((error) => {
          alert('error:' + error)
        })
      this.$message({
        type: 'success',
        message: '删除成功!'
      });
    },
    handleImageUploadSuccess(file) {
      this.template.thumbnail_url = file.url
      this.image_visible = true
    },
    handleExceed(files, fileList) {
      this.$message.warning(`当前限制选择 1 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
    },
    checkType(file,fileList) {
      this.template.thumbnail=file
    },
    reload () {
      location.reload()
    },
    CreateNewType: function() {
      const data = {
        name: this.type_name.name
      }
      Axios({
        url: '/property-types/',
        method: 'post',
        data: data,
        headers: {
          Authorization: 'Bearer ' + this.$store.getters.getUserAccessToken
        }
      })
        .then((response) => {
          this.type_dialogFormVisible = false
          this.reload()
        })
        .catch((error) => {
          alert('error:' + error)
        })
      this.type_dialogFormVisible = false
    },
    CreateNewTemplate: function() {
      var json = {}
      for(var i=0;i<this.template_fields.length;i++)
      {
        json[this.template_fields[i].name]=this.template_fields[i].details
      }
      this.template.fields = JSON.stringify(json)
      let data=new FormData();
      data.append('name', this.template.name)
      data.append('type', this.template.type)
      data.append('thumbnail', this.template.thumbnail.raw)
      data.append('fields', this.template.fields)
      Axios({
        url: '/property-templates/',
        method: 'post',
        data: data,
        headers: {
          Authorization: 'Bearer ' + this.$store.getters.getUserAccessToken
        }
      })
        .then((response) => {
          this.template_dialogFormVisible = false
          this.reload()
        })
        .catch((error) => {
          alert('error:' + error)
        })
      this.template_dialogFormVisible = false
    },
    enter: function (row) {
      if(row.type)
      {
        this.$router.push({ name: 'property-templates', params: { templateId: row.id } })
      }
    },
    searchAndFilter: function (select, input) {
      this.select = select
      this.input = input
      this.changePage(1)
    },
    changePage: function (page) {
      Axios.get('/property-types', {
        params: {
          page: page
        }
      })
        .then((response) => {
          this.property_type_list = response.data
        }).catch((error) => {
          this.$alert(error.response.data)
        })
    }
  }
}
</script>
