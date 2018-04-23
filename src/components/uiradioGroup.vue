<template>
  <div :class="classes" :name="name">
    <slot></slot>
  </div>
</template>
<script>
  const prefixCls = 'ivu-radio-group';
  let seed = 0;
  const now = Date.now();
  const getUuid = () => `ivuRadioGroup_${now}_${seed++}`;
  export default {
    props: {
      value: {
        type: [String, Number],
        default: ''
      },
      vertical: {
        type: Boolean,
        default: false
      },
      name: {
        type: String,
        default: getUuid
      }
    },
    data () {
      return {
        currentValue: this.value,
        childrens: []
      };
    },
    computed: {
      classes () {
        return [
          `${prefixCls}`,
          {
            //[`${prefixCls}-${this.size}`]: !!this.size,
           // [`ivu-radio-${this.size}`]: !!this.size,
            [`${prefixCls}-${this.type}`]: !!this.type,
            [`${prefixCls}-vertical`]: this.vertical
          }
        ];
      }
    },
    mounted () {
      this.updateValue();
    },
    methods: {
      updateValue () {
        //this.childrens = findComponentsDownward(this, 'Radio');
        if (this.childrens) {
          this.childrens.forEach(child => {
            child.currentValue = this.value === child.label;
            child.group = true;
          });
        }
      },
      change (data) {
        this.currentValue = data.value;
        this.updateValue();
        this.$emit('input', data.value);
        this.$emit('on-change', data.value);
       // this.dispatch('FormItem', 'on-form-change', data.value);
      }
    },
    watch: {
      value () {
        this.currentValue = this.value;
        this.updateValue();
      }
    }
  };
</script>
<style scoped>
  .ivu-radio-group {
    display: inline-block;
    font-size: 12px;
    vertical-align: middle;
  }

</style>
