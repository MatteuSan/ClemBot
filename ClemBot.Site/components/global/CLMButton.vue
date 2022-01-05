<template>
  <button :class="`clm-button${type ? ' ' + parseTypes(type) : ''}`">
    <i v-if="icon || $slots.icon" class="clm-button__icon">
      <slot name="icon"><b-icon :icon="icon" /></slot>
    </i>
    <span v-if="label || $slots.default" class="clm-button__label">
      <slot>{{ label }}</slot>
    </span>
  </button>
</template>

<script lang="ts">
export default {
  name: 'CLMButton',
  props: {
    label: {
      default: null,
      type: String,
    },
    icon: {
      default: null,
      type: String,
    },
    type: {
      default: 'text',
      type: String,
    },
  },
  methods: {
    parseTypes(types: string) {
      const VALID_BUTTON_TYPES = [
        'text',
        'outlined',
        'filled',
        'inverted',
        'raised',
        'icon-only',
      ]
      if (types) {
        types.split(' ').forEach((type) => {
          if (!VALID_BUTTON_TYPES.includes(type)) {
            throw new Error(
              `Invalid type ${type}! Please use one of the following valid types: ${VALID_BUTTON_TYPES.join(
                ', '
              )}.`
            )
          }
        })
      }
      const finalTypes: Array<string> = []
      types.split(' ').forEach((type) => {
        if (type === 'text') {
          finalTypes.push('')
        }
        finalTypes.push('clm-button--' + type)
      })
      return finalTypes.join(' ')
    },
  },
}
</script>

<style lang="scss" scoped>
@use '~@matteusan/sentro' with (
  $prefix: 'clm',
  $context: 'token'
);
@use 'sass:map';

@mixin style($color-map) {
  $fill: map.get($color-map, 'fill');
  $ink: map.get($color-map, 'ink');
  $border: map.get($color-map, 'border');

  background: sentro.key-create('button-fill', $fill);
  color: sentro.key-create('button-ink', $ink);
  border: 1px solid sentro.key-create('button-border', $border);
}

@mixin extend($color-map) {
  $fill: map.get($color-map, 'fill');
  $ink: map.get($color-map, 'ink');
  $border: map.get($color-map, 'border');

  @include sentro.key-bind('button-fill', $fill);
  @include sentro.key-bind('button-ink', $ink);
  @include sentro.key-bind('button-border', $border);
}

.clm-button {
  width: 100%;
  min-width: 67px;
  max-width: max-content;
  margin: 0;
  padding: 0.4rem 0.6rem;

  display: inline-flex;
  flex-flow: row nowrap;
  justify-content: center;
  align-items: center;

  border-radius: 0.3rem;

  user-select: none;
  cursor: pointer;
  @include sentro.prefix(transition, all 0.1s ease);

  > * + * {
    margin-left: 0.4rem;
  }

  .clm-button__icon {
    font-size: sentro.px-to-rem(22px);

    * {
      font-size: sentro.px-to-rem(22px);
      /// @fallback
      width: sentro.px-to-rem(22px);
      height: sentro.px-to-rem(22px);
    }
  }

  .clm-button__label {
    font-size: sentro.px-to-rem(16px);
    font-weight: 700;
    line-height: sentro.px-to-rem(20px);
  }

  &.clm-button--icon-only {
    width: calc(24px + 0.6rem);
    min-width: auto !important;
    height: calc(24px + 0.4rem);
  }

  &.clm-button--raised {
    @include sentro.elevation-apply(1);

    &:active {
      @include sentro.elevation-apply(2);
    }
  }

  // Variants
  &.clm-button--text {
    @include style(
      (
        'fill': rgba(0 0 0 / 0),
        'ink': sentro.token-get('primary'),
        'border': rgba(0 0 0 / 0),
      )
    );

    &:hover,
    &:focus {
      @include extend(
        (
          'fill': rgba(255 255 255 / 15%),
          'ink': sentro.token-get('primary'),
          'border': rgba(255 255 255 / 1.5%),
        )
      );
    }

    &:active {
      @include extend(
        (
          'fill': rgba(255 255 255 / 20%),
          'ink': sentro.token-get('primary-light'),
          'border': rgba(255 255 255 / 2%),
        )
      );
    }

    &:disabled {
      @include extend(
        (
          'fill': rgba(0 0 0 / 0),
          'ink': sentro.token-get('primary-dark'),
          'border': rgba(0 0 0 / 0),
        )
      );
    }
  }

  &.clm-button--outlined {
    @include style(
      (
        'fill': rgba(0 0 0 / 0),
        'ink': sentro.token-get('primary'),
        'border': sentro.token-get('primary'),
      )
    );

    &:hover,
    &:focus {
      @include extend(
        (
          'fill': rgba(255 255 255 / 15%),
          'ink': sentro.token-get('primary'),
          'border': sentro.token-get('primary'),
        )
      );
    }

    &:active {
      @include extend(
        (
          'fill': rgba(255 255 255 / 20%),
          'ink': sentro.token-get('primary-light'),
          'border': sentro.token-get('primary-light'),
        )
      );
    }

    &:disabled {
      @include extend(
        (
          'fill': rgba(0 0 0 / 0),
          'ink': sentro.token-get('primary-dark'),
          'border': sentro.token-get('primary-dark'),
        )
      );
    }
  }

  &.clm-button--filled {
    @include style(
      (
        'fill': sentro.token-get('primary'),
        'ink': sentro.token-get('primary-ink'),
        'border': sentro.token-get('primary'),
      )
    );

    &:hover,
    &:focus {
      @include extend(
        (
          'fill': sentro.token-get('primary'),
          'ink': sentro.token-get('primary-ink'),
          'border': sentro.token-get('primary'),
        )
      );
    }

    &:active {
      @include extend(
        (
          'fill': sentro.token-get('primary-light'),
          'ink': sentro.token-get('primary-ink'),
          'border': sentro.token-get('primary-light'),
        )
      );
    }

    &:disabled {
      @include extend(
        (
          'fill': sentro.token-get('primary-dark'),
          'ink': sentro.token-get('primary-ink'),
          'border': sentro.token-get('primary-dark'),
        )
      );
    }
  }
}
</style>
