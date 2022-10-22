<template>
  <FormProvider :form="form">
    <SchemaField>
      <SchemaArrayField
          name="array"
          x-decorator="FormItem"
          x-component="ArrayTable"
          :x-component-props="{
          pagination: { pageSize: 10 },
          scroll: { x: 800 },
        }"
      >
        <SchemaObjectField>
          <SchemaVoidField
              x-component="ArrayTable.Column"
              :x-component-props="{ width: 80, title: 'Index', align: 'center' }"
          >
            <SchemaVoidField
                x-decorator="FormItem"
                x-component="ArrayTable.Index"
            />
          </SchemaVoidField>
          <SchemaVoidField
              x-component="ArrayTable.Column"
              :x-component-props="{ title: 'A1', dataIndex: 'a1', width: 200 }"
          >
            <SchemaStringField
                x-decorator="Editable"
                name="a1"
                :required="true"
                x-component="Input"
            />
          </SchemaVoidField>
        </SchemaObjectField>
      </SchemaArrayField>
    </SchemaField>
  </FormProvider>
</template>

<script lang="ts" setup>
import { createForm } from "@formily/core";
import { FormProvider, createSchemaField } from "@formily/vue";
import { FormItem, ArrayTable, Input, Editable } from "@formily/antdv-x3";

const {
  SchemaField,
  SchemaObjectField,
  SchemaStringField,
  SchemaVoidField,
  SchemaArrayField,
} = createSchemaField({
  components: {
    FormItem,
    ArrayTable,
    Input,
    Editable,
  },
});

const form = createForm();
form.setInitialValues({
  array: range(15),
});

function range(count: number) {
  return Array.from(new Array(count)).map((_, key) => ({
    a1: `id: ${key}`,
  }));
}
</script>