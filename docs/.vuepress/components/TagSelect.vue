<template>
  <div class="component_tag_select">
    <div class="tags">
      <div
        class="tag_container"
        v-for="(item, index) in tagsList"
        :key="item.name"
      >
        <div
          class="tag"
          :class="{
            active: tagActive === index,
            mask: tagActive !== index && tagActive !== null,
          }"
          @click="
            () => {
              tagActive = index;
            }
          "
        >
          <div
            class="title text-cut"
            :class="chooseText[item.name]?.join(',') ? 'text_blue' : ''"
          >
            {{ chooseText[item.name]?.join(",") || item.title }}
          </div>
          <div class="triangles"></div>
        </div>
      </div>
    </div>
    <div class="custom_popup active" v-if="tagActive !== null">
      <div class="white_bg">
        <div class="content_list">
          <div
            class="content_item"
            @click="clickFn(item, tagsList[tagActive].name)"
            :class="{
              active: choose[tagsList[tagActive].name]?.includes(item.value),
            }"
            v-for="item in tagsList[tagActive].children"
            :key="item.value"
          >
            {{ item.lable }}
          </div>
        </div>
        <div class="btns">
          <div class="btn" @click="cancel">重置</div>
          <div class="btn" @click="confirm">确认</div>
        </div>
      </div>
    </div>
    <div
      class="tag_select_mask"
      :class="{ active: tagActive !== null }"
      @click="close"
    ></div>
  </div>
</template>
<script>
export default {
  props: {
    tagsList: {
      default: [],
    },
    value: {
      default: {},
    },
  },
  data() {
    return {
      choose: {},
      chooseText: {},
      tagActive: null,
    };
  },
  watch: {
    value: function (newVal) {
      const keys = Object.keys(newVal);
      let newChoose = {};
      let newChooseText = {};
      let tagsChildren = {};
      this.tagsList.map((item) => {
        tagsChildren[item.name] = item.children;
      });
      keys.map((key) => {
        newChoose[key] = newVal[key] ? newVal[key].split(",") : [];
        let text = [];
        newChoose[key].map((item) => {
          let { lable } = this.getItemFromValue(tagsChildren[key], item);
          text.push(lable);
        });
        newChooseText[key] = text;
      });
      this.choose = newChoose;
      this.chooseText = newChooseText;
    },
  },
  methods: {
    getItemFromValue(arr, val, valKey = "value") {
      for (let i = 0; i < arr.length; i++) {
        const item = arr[i];
        if (item[valKey] === val) {
          return item;
        }
      }
    },
    reset(newVal) {
      let copyVal = JSON.parse(JSON.stringify(newVal));
      for (let key in copyVal) {
        copyVal[key] = copyVal[key] ? copyVal[key].split(",") : [];
      }
      this.choose = copyVal;
    },
    pxove(arr, str) {
      let index = arr.indexOf(str);
      let newArr = [];
      if (index != -1 && index != 0) {
        newArr = arr.slice(0, index);
        newArr.push(...arr.slice(index + 1, arr.length));
      } else if (index != -1 && index == 0) {
        arr.shift();
        newArr = [...arr];
      } else {
        newArr = [...arr];
      }
      return newArr;
    },
    clickFn(item, name) {
      let newVal = this.choose[name] || [];
      if (newVal.includes(item.value)) {
        newVal = this.pxove(newVal, item.value);
      } else {
        newVal.push(item.value);
      }
      this.choose = Object.assign({}, this.choose, {
        [name]: newVal,
      });
    },
    confirm() {
      const keys = Object.keys(this.choose);
      let newObj = {};
      keys.map((key) => {
        newObj[key] = this.choose[key]?.join(",") || "";
      });
      this.tagActive = null;
      console.log("newObj", newObj);
      this.$emit("confirm", newObj);
    },
    cancel() {
      this.choose = {};
    },
    close() {
      this.tagActive = null;
      this.reset(this.value);
    },
  },
};
</script>
<style lang="less">
.component_tag_select {
    position: relative;
    margin-top: .3rem;
    .tags {
        width: 100%;
        height: .8rem;
        position: relative;
        z-index: 803;
        display: flex;
        overflow-x: auto;
        .tag_container {
            display: flex;
            padding-bottom: .2rem;
            margin-right: .2rem;
            .tag {
                position: relative;
                min-width: 2.1rem;
                height: .6rem;
                padding: 0 .3rem; 
                display: flex;
                justify-content: center;
                align-items: center;
                background-color: #ededed;
                border-radius: .3rem;
                &.active {
                    background-color: #fff;
                    border-radius: .3rem .3rem 0 0;
                    &::before {
                        position: absolute;
                        display: block;
                        content: '';
                        background-color: #fff;
                        height: .3rem;
                        width: 100%;
                        left: 0;
                        bottom: 0;
                        transform: translateY(100%);
                    }
                }
                &.mask {
                    &::after {
                        content: '';
                        display: block;
                        width: 100%;
                        height: 100%;
                        position: absolute;
                        top: 0;
                        left: 0;
                        border-radius: .3rem;
                        background: rgba(0,0,0,0.3);
                    }
                }
                .title {
                    &.text_blue {
                        color: green;
                        width: 2.1rem;
                        .tag_select_choose_name {
                            width: calc(100%);
                            text-align: center;
                        }
                    }
                }
            }
            .triangles{
                width: 0;
                height: 0;
                border-top: .1rem solid #666;
                border-bottom: .1rem solid transparent;
                border-left: .1rem solid transparent;
                border-right: .1rem solid transparent;
                margin-top: .08rem;
                margin-left: .18rem;
            }
        }
    }
    .custom_popup {
        position: absolute;
        top: 100%;
        left: 0;
        width: calc(100vw - .6rem);
        max-width: calc(414px - .6rem);
        z-index: 802;
        box-sizing: border-box;
        display: none;
        transform: translateY(-.2rem);
        &.active {
            display: block;
        }
        .white_bg {
            width: 100%;
            box-sizing: border-box;
            background-color: #fff;
            border-radius: .2rem .2rem .2rem .2rem;
            padding: .38rem .2rem;
            .content_list {
                display: flex;
                flex-wrap: wrap;
                margin-left: -.68rem;
                margin-top: -.24rem;
                .content_item {
                    padding: 0 4px;
                    font-size: .28rem;
                    color: #666;
                    margin-left: .68rem;
                    margin-top: .24rem;
                    &.active {
                        color: green;
                    }
                }
            }
            .btns {
                margin-top: .4rem;
                padding-top: .4rem;
                border-top: 1px solid #eee;
                display: flex;
                .btn {
                    border-radius: .35rem;
                    height: .7rem;
                    line-height: .7rem;
                    width: calc((100% - .64rem) / 2);
                    border: solid 1px green;
                    text-align: center;
                    font-size: .28rem;
                    &:nth-child(2) {
                        margin-left: .64rem;
                    }
                    &:first-child {
                        color: green;
                        background-color: #fff;
                    }
                    &:last-child {
                        color: #fff;
                        background-color: green;
                    }
                }
            }
        }
    }
    .tag_select_mask {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,0.3);
        z-index: 801;
        display: none;
        &.active {
            display: block;
        }
    }
}
</style>