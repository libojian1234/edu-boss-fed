<template>
  <div class="resourceList">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :model="form" ref="form" label-width="80px">
          <el-form-item label="资源名称" prop="name">
            <el-input v-model="form.name"></el-input>
          </el-form-item>
          <el-form-item label="资源路径" prop="url">
            <el-input v-model="form.url"></el-input>
          </el-form-item>
          <el-form-item label="资源分类" prop="categoryId">
            <el-select v-model="form.categoryId" placeholder="请选择资源分类" clearable>
              <el-option
                :label="item.name"
                :value="item.id"
                v-for="item in resourceCategories"
                :key="item.id"
              ></el-option>
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSubmit" :disabled="isLoading">查询搜索</el-button>
            <el-button @click="onReset" :disabled="isLoading">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
      <el-table
        :data="resources"
        style="width: 100%; margin-bottom: 20px"
        v-loading="isLoading"
      >
        <el-table-column
          type="index"
          label="编号">
        </el-table-column>
        <el-table-column
          prop="name"
          label="资源名称"
          width="180">
        </el-table-column>
        <el-table-column
          prop="url"
          label="资源路径">
        </el-table-column>
        <el-table-column
          prop="description"
          label="描述">
        </el-table-column>
        <el-table-column
          prop="createdTime"
          label="添加时间">
        </el-table-column>
        <el-table-column label="操作" :min-width="100">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.row)">编辑</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
      <!--
        total 总记录数
        page-size 每页大小
        分页组件会自动根据 total 和 page-size 计算出一共分多少页
      -->
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page.sync="form.current"
        :disabled="isLoading"
        :page-sizes="[5, 10, 20]"
        :page-size="form.size"
        layout="total, sizes, prev, pager, next, jumper"
        :total="totalCount">
      </el-pagination>
    </el-card>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Form } from 'element-ui'
import { getResourcePages } from '@/services/resource'
import { getResourceCategories } from '@/services/resource-categore'

export default Vue.extend({
  name: 'ResourceList',
  data () {
    return {
      resources: [],
      form: {
        name: '',
        url: '',
        categoryId: null, // 资源分类
        current: 1, // 默认查询第1页数据
        size: 5 // 每页大小
      },
      totalCount: 0,
      resourceCategories: [], // 资源分类列表
      isLoading: true
    }
  },
  created () {
    this.loadResource()
    this.loadResourceCategories()
  },
  methods: {
    async loadResource () {
      this.isLoading = true // 展示加载中状态
      const { data } = await getResourcePages(this.form)
      if (data.code === '000000') {
        this.resources = data.data.records
        this.totalCount = data.data.total
      }
      this.isLoading = false // 关闭加载中状态
    },
    async loadResourceCategories () {
      const { data } = await getResourceCategories()
      if (data.code === '000000') {
        this.resourceCategories = data.data
      }
    },
    onSubmit () {
      this.form.current = 1 // 刷选查询从第1页开始
      this.loadResource()
    },
    handleEdit () {
      console.log('handleEdit')
    },
    handleDelete () {
      console.log('handleDelete')
    },
    handleSizeChange (val: number) {
      console.log(`每页 ${val} 条`)
      this.form.current = 1 // 每页大小改变重新查询第1页数据
      this.form.size = val
      this.loadResource()
    },
    handleCurrentChange (val: number) {
      console.log(`当前页: ${val}`)
      // 请求获取对应页码的数据
      this.form.current = val // 修改当前页码
      this.loadResource()
    },
    onReset () {
      (this.$refs.form as Form).resetFields()
      this.form.current = 1 // 重置回到第1页
      this.loadResource()
    }
  }
})
</script>

<style lange="scss" scoped></style>
