<template>
  <div class="p-4">
    <t-card class="mb-4">
      <el-row>
        <basic-form :schemas="formSchema" inline label-width="80px">
          <template #action>
            <el-row>
              <!-- <el-button type="primary" @click="() => handleGetHeight()">获取高度</el-button> -->
            </el-row>
          </template>
        </basic-form>
      </el-row>
    </t-card>
    <t-card header="milkdown编辑器" tips="markdown语法，所见即所得">
      <milkdown
        v-if="form.show"
        ref="editor"
        :readonly="form.readonly"
        :default-value="'# 欢迎使用toimc管理后台项目'"
      ></milkdown>
    </t-card>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from 'vue'
  import { FormSchema } from '@/components/Form/types/types'
  // import { ElMessageBox } from 'element-plus'

  export default defineComponent({
    setup() {
      const editor = ref()

      let form = reactive({
        show: true, // 显示editor,
        readonly: false // 只读模式
      })
      
      const handleToggleShow = (val) => {
        val === true ? editor.value : !editor.value
        form.show = val
      }

      const handleToggleReadonly = (val) => {
        val === true ? editor.value : !editor.value
        form.readonly = val
      }

      const formSchema: FormSchema[] = reactive([
        {
          component: 'switch',
          value: form.show,
          label: '是否显示',
          prop: 'isShow',
          events: {
            change: handleToggleShow
          }
        },
        {
          component: 'switch',
          value: form.readonly,
          label: '只读模式',
          prop: 'isReadonly',
          events: {
            change: handleToggleReadonly
          }
        }
      ] as FormSchema[])

      return {
        editor,
        form,
        formSchema
      }
    }
  })
</script>

<style scoped></style>
