<template>
  <n-space vertical :size="12">
    <n-data-table
        size="small"
        :columns="columns"
        :data="data"
        :pagination="pagination"
    />
    <n-data-table
        size="large"
        :columns="columns"
        :data="data"
        :pagination="pagination"
    />
  </n-space>
  <n-h3>LoadingBar</n-h3>
  <n-button type="primary" @click="handleShowLoadingBar">
    useLoadingBar
  </n-button>
  <n-button type="primary" @click="handleShowMessage">
    useMessage
  </n-button>
  <n-button type="primary" @click="handleShowNotification">
    useNotification
  </n-button>
  <n-button type="primary" @click="handleShowDialog">
    useDialog
  </n-button>
</template>

<script setup>
import {h} from "vue";
import {NTag, NButton, NIcon} from "naive-ui";
import {AccessPoint} from '@vicons/tabler'
import {useLoadingBar, useMessage, useNotification, useDialog} from 'naive-ui'

const loadingBar = useLoadingBar()
const handleShowLoadingBar = () => {
  loadingBar.start()
}
const message = useMessage()
const handleShowMessage = () => {
  message.success('I can use message')
}
const notification = useNotification()
const handleShowNotification = () => {
  notification.success({
    content: 'Will be success',
    meta: 'I think so',
  })
}
const dialog = useDialog()
const handleShowDialog = () => {
  dialog.success({
    title: 'Success use dialog',
    content: 'Cool',
    positiveText: 'Wow!',
  })
}
const createColumns = ({
                         sendMail
                       }) => {
  return [
    {
      title: "Name",
      key: "name"
    },
    {
      title: "Age",
      key: "age"
    },
    {
      title: "Address",
      key: "address"
    },
    {
      title: "Tags",
      key: "tags",
      render(row) {
        const tags = row.tags.map((tagKey) => {
          return h(NTag, {
            style: {
              marginRight: "6px"
            },
            type: "info",
            bordered: false
          }, {
            default: () => tagKey
          });
        });
        return tags;
      }
    },
    {
      title: "Action",
      key: "actions",
      render(row) {
        return h(
            NButton,
            {
              size: "small",
              type: "primary"
            }, {
              icon: () => h(NIcon,
                  {size: "24"},
                  {
                    default: () => h(AccessPoint)
                  })
            }
        );
      }
    }
  ];
};

const createData = () => [
  {
    key: 0,
    name: "John Brown",
    age: 32,
    address: "New York No. 1 Lake Park",
    tags: ["nice", "developer"]
  },
  {
    key: 1,
    name: "Jim Green",
    age: 42,
    address: "London No. 1 Lake Park",
    tags: ["wow"]
  },
  {
    key: 2,
    name: "Joe Black",
    age: 32,
    address: "Sidney No. 1 Lake Park",
    tags: ["cool", "teacher"]
  }
];

const data = createData()
const columns = createColumns
({
  sendMail(rowData) {
    alert("send mail to " + rowData.name);
  }
})
const pagination = {
  pageSize: 10
}
</script>