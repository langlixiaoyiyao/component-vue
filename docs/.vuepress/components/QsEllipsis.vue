<template>
  <div class="component_qs_ellipsis">
    <div class="content_container">
      <div ref="showRef">{{ end ? showText : ""}}<span class="span-click" v-if="end && cut" @click="handleClick">{{open ? closeText : expanText}}</span>
      </div>
      <div class="dont-show" ref="hideRef"></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    content: String,
    line: {
      default: 3,
    },
    expanText: {
      default: "展开",
    },
    closeText: {
      default: "收起",
    },
  },
  data() {
    return {
      cutText: "",
      showText: "",
      end: false,
      cut: false,
      maxHeight: 0,
      open: false,
    };
  },
  components: {},
  methods: {
    handleClick() {
      if (this.open) {
        this.open = false;
        this.showText = this.cutText;
      } else {
        this.open = true;
        this.showText = this.content;
      }
    },
    ifNeedCut() {
      this.$refs.hideRef.innerText = this.content;
      if (this.$refs.hideRef.offsetHeight <= this.maxHeight) {
        this.end = true;
        this.showText = this.content;
        return false;
      }
      this.cut = true;
      return true;
    },
    computedText(start, end) {
      const middle = Math.floor((start + end) / 2);
      let text = this.content.slice(0, middle);
      if (end - start <= 1) {
        this.showText = text + "...";
        this.cutText = text + "...";
        this.end = true;
        return;
      }
      this.$refs.hideRef.innerText = text + "..." + this.expanText;
      if (this.$refs.hideRef.offsetHeight > this.maxHeight) {
        this.computedText(start, middle);
      } else {
        this.computedText(middle, end);
      }
    },
    replacePx(str) {
      return str.replace("px", "") - 0;
    },
  },
  mounted() {
    const computedStyle = window.getComputedStyle(this.$refs.showRef);
    const styleArray = Array.from(computedStyle);
    styleArray.forEach((value) => {
      this.$refs.hideRef.style[value] = computedStyle.getPropertyValue(value);
    });
    this.maxHeight =
      this.replacePx(computedStyle.getPropertyValue("line-height")) *
        (this.line + 0.5) +
      this.replacePx(computedStyle.getPropertyValue("top-border-width")) +
      this.replacePx(computedStyle.getPropertyValue("bottom-border-width"));
      console.log(computedStyle.getPropertyValue("line-height")
      )
    this.ifNeedCut() && this.computedText(0, this.content.length);
  },
};
</script>
<style lang="less">
.component_qs_ellipsis {
  .content_container {
    position: relative;
    white-space: pre-wrap;
    line-height: 1.7;
    .dont-show {
      position: absolute !important;
      top: -999px !important;
      left: -999px !important;
      z-index: -999 !important;
      height: auto !important;
      max-height: unset !important;
      min-height: unset !important;
    }
  }
  .span-click {
      color: #70B64D;
  }
}
</style>