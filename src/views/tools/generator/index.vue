<template>
  <div class="generator-code">
    <el-row>
      <el-col :span="24">
        <el-card class="box-card">
          <div class="search">
            <el-input
              v-model="searchVal"
              placeholder="请按表名进行搜索"
              class="search-input margin-box"
              @keyup.native.enter="search"
            ></el-input>
            <el-button icon="el-icon-search" class="margin-box" @click="search" circle></el-button>
            <el-button
              type="success"
              icon="el-icon-refresh"
              class="margin-box"
              @click="refresh"
              circle
              title="重置"
            ></el-button>
          </div>
          <el-table :data="generateCodeList" style="width: 100%" highlight-current-row stripe>
            <el-table-column type="expand">
              <template slot-scope="props">
                <el-form label-position="left" inline class="demo-table-expand">
                  <el-form-item label="备注" class="expand-line">
                    <span>{{ props.row.remark ? props.row.remark : "无" }}</span>
                  </el-form-item>
                </el-form>
              </template>
            </el-table-column>
            <el-table-column label="表名" show-overflow-tooltip>
              <template slot-scope="scope">
                <span style="margin-left: 10px">{{ scope.row.tableName }}</span>
              </template>
            </el-table-column>
            <el-table-column label="数据库引擎" show-overflow-tooltip>
              <template slot-scope="scope">
                <div slot="reference">{{ scope.row.engine }}</div>
              </template>
            </el-table-column>
            <el-table-column label="字符编码集" show-overflow-tooltip>
              <template slot-scope="scope">
                <div slot="reference">{{ scope.row.coding }}</div>
              </template>
            </el-table-column>
            <el-table-column label="创建日期" width="180">
              <template slot-scope="scope">
                <div slot="reference" class="name-wrapper">{{ scope.row.createTime }}</div>
              </template>
            </el-table-column>
            <el-table-column label="操作" width="200" align="center" fixed="right">
              <template slot-scope="scope">
								<el-button
								  slot="reference"
								  type="text"
								  @click="$router.push({ path: `/home/preview?tableName=${scope.row.tableName}` })"
								>预览</el-button>
								<el-button
								  slot="reference"
								  type="text"
								  @click="downloadCode(scope.row)"
								>下载</el-button>
								<el-button
								  slot="reference"
								  type="text"
								  @click="editGeneratorCode(scope.row)"
								>编辑</el-button>
                <el-button
                  slot="reference"
                  type="text"
                  @click="generateCode(scope.row)"
                >生成</el-button>
              </template>
            </el-table-column>
          </el-table>
          <pagination
            ref="pagination"
            :get-data="getGenerateCodeList"
            :now-page.sync="nowPage"
            :now-size.sync="nowSize"
            :total="totalElements"
          />
        </el-card>
      </el-col>
    </el-row>
    <GeneratorBox ref="form" />
  </div>
</template>

<script>
import Initial from "./js/initial";
import Operation from "./js/operation";
import Property from "./js/property";
import GeneratorBox from "./components/form";
export default {
  mixins: [Initial, Operation, Property],
  components: { GeneratorBox }
};
</script>

<style lang="scss" scoped>
</style>
