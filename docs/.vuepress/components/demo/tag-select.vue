<template>
  <tag-select
    :tagsList="tagsList"
    :value="tagSearch"
    @confirm="confirm"
  ></tag-select>
</template>
<script>
export default {
  data() {
    return {
      tagsList: [
        {
          title: "图书分类",
          name: "color",
          children: [
            {
              lable: "绘本图画",
              value: "red",
            },
            {
              lable: "社会科学",
              value: "green",
            },
            {
              lable: "自然科学",
              value: "blue",
            },
            {
              lable: "中外文学",
              value: "yellow",
            },
            {
              lable: "综合百科",
              value: "purple",
            },
          ],
        },
        {
          title: "适读年级",
          name: "reading_level",
          children: [
            {
              lable: "0-3岁",
              value: "1",
            },
            {
              lable: "幼儿园",
              value: "2",
            },
            {
              lable: "1-2年级",
              value: "3",
            },
            {
              lable: "3-4年级",
              value: "4",
            },
            {
              lable: "5-6年级",
              value: "5",
            },
            {
              lable: "初中",
              value: "6",
            },
            {
              lable: "高中",
              value: "7",
            },
            {
              lable: "教师家长",
              value: "8",
            },
          ],
        },
      ],
      tagSearch: {},
    };
  },
  methods: {
    confirm(obj) {
      console.log(obj);
    },
  },
};
</script>