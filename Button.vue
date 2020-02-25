<script>
  export default {
    name: 'c-button',
    props: {
      to: {
        type: [String, Object],
        required: false,
        default: ''
      },
      actions: {
        type: Array,
        required: false,
        default () {
          return []
        }
      },
      disabled: {
        type: Boolean,
        required: false,
        default: false
      },
      replace: {
        type: Boolean,
        required: false,
        default: false
      },
      color: {
        type: String,
        required: false,
        default: 'blue',
        validator (color) {
          const colors = ['blue', 'gray']

          return colors.includes(color)
        }
      },
      icon: {
        type: Boolean,
        required: false,
        default: false
      },
      large: {
        type: Boolean,
        required: false,
        default: false
      },
      prependIcon: {
        type: Boolean,
        required: false,
        default: false
      },
      appendIcon: {
        type: Boolean,
        required: false,
        default: false
      },
      round: {
        type: Boolean,
        required: false,
        default: false
      }
    },
    computed: {
      nuxtLinkOptions () {
        const {to, disabled, replace} = this

        return {
          event: to && !disabled ? 'click' : '',
          tag: to ? 'a' : 'button',
          to,
          disabled,
          replace
        }
      }
    }
  }
</script>

<template>
  <nuxt-link v-bind="nuxtLinkOptions"
             :class="{
               [`c-button_${color}`]: true,
               'c-button_disabled': disabled,
               'c-button_icon': icon,
               'c-button_large': large,
               'c-button_prepend_icon': prependIcon,
               'c-button_append_icon': appendIcon,
               'c-button_round': round
             }"
             class="c-button">
    <!--<div v-if="round">-->
    <!--<div v-for="action in actions"-->
    <!--:key="action.value"-->
    <!--class="c-button__list">-->
    <!--<div class="c-button__list-icon">-->
    <!--<svg-icon name="plus"/>-->
    <!--</div>-->
    <!--<span class="c-button__list-text">-->
    <!--{{ action.name }}-->
    <!--</span>-->
    <!--</div>-->
    <!--</div>-->
    <span v-if="prependIcon && $slots.icon"
          class="c-button__icon">
      <slot name="icon"/>
    </span>
    <span v-if="round && $slots.icon"
          class="c-button__icon">
      <slot name="icon"/>
    </span>
    <span class="c-button__text">
      <slot/>
    </span>
    <span v-if="appendIcon && $slots.icon"
          class="c-button__icon">
      <slot name="icon"/>
    </span>
  </nuxt-link>
</template>

<style lang="scss" src="./button.scss"/>