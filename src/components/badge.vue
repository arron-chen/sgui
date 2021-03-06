<template>
    <span v-if="dot" :class="classes" ref="badge">
        <slot></slot>
        <sup :class="dotClasses" v-show="badge"></sup>
    </span>
    <span v-else :class="classes" ref="badge">
          <slot></slot>
          <sup v-if="count" :class="countClasses" v-show="badge">{{ finalCount }}</sup>
    </span>
</template>
<script>
  const prefixCls = 'ivu-badge';
  export default {
    name: 'Badge',
    props: {
      count: [Number, String],
      dot: {
        type: Boolean,
        default: false
      },
      overflowCount: {
        type: [Number, String],
        default: 99
      },
      className: String
    },
    computed: {
      classes () {
        return `${prefixCls}`;
      },
      dotClasses () {
        return `${prefixCls}-dot`;
      },
      countClasses () {
        return [
          `${prefixCls}-count`,
          {
            [`${this.className}`]: !!this.className,
            [`${prefixCls}-count-alone`]: this.alone
          }
        ];
      },
      finalCount () {
        return parseInt(this.count) >= parseInt(this.overflowCount) ? `${this.overflowCount}+` : this.count;
      },
      badge () {
        let status = false;
        if (this.count) {
          status = !(parseInt(this.count) === 0);
        }
        if (this.dot) {
          status = true;
          if (this.count !== null) {
            if (parseInt(this.count) === 0) {
              status = false;
            }
          }
        }
        return status;
      },
      alone () {
        return this.$slots.default === undefined;
      }
    }
  };
</script>
<style scoped>
  *{
    box-sizing: border-box;
  }
  .ivu-badge {
    position: relative;
    display: inline-block;
    line-height: 1;
    vertical-align: middle;
  }
  .ivu-badge-dot {
    position: absolute;
    -webkit-transform: translateX(-50%);
    transform: translateX(-50%);
    -webkit-transform-origin: 0 center;
    transform-origin: 0 center;
    top: -4px;
    right: -8px;
    height: 8px;
    width: 8px;
    border-radius: 100%;
    background: #ed3f14;
    z-index: 10;
    box-shadow: 0 0 0 1px #fff;
  }
  .ivu-badge-count {
    position: absolute;
    -webkit-transform: translateX(50%);
    transform: translateX(50%);
    top: -10px;
    right: 0;
    height: 20px;
    border-radius: 10px;
    min-width: 20px;
    background: #ed3f14;
    border: 1px solid transparent;
    color: #fff;
    line-height: 18px;
    text-align: center;
    padding: 0 6px;
    font-size: 12px;
    white-space: nowrap;
    -webkit-transform-origin: -10% center;
    transform-origin: -10% center;
    z-index: 10;
    box-shadow: 0 0 0 1px #fff;
  }
  .ivu-badge-count-alone {
    top: auto;
    display: block;
    position: relative;
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }
</style>
