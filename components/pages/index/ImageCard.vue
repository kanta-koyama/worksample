<template>
  <div class="c-image_card">
    <img :src="path" alt="" />
    <span class="c-image_card_setting" @click="showPopup">設定</span>
    <div v-if="popupVisibleFlg" class="c-image_card_popup">
      <ul>
        <li>
          <span
            class="c-image_card_popup_button left"
            @click="handleClickMoveItemLeft"
            >左へ移動</span
          >
        </li>
        <li>
          <span
            class="c-image_card_popup_button right"
            @click="handleClickMoveItemRight"
            >右へ移動</span
          >
        </li>
        <li>
          <span
            class="c-image_card_popup_button delete"
            @click="handleClickDeleteItem"
            >画像を削除</span
          >
        </li>
        <li>
          <span class="c-image_card_popup_button close" @click="hidePopup"
            >閉じる</span
          >
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageCardComponent',
  props: {
    index: {
      type: Number,
      default: 0,
    },
    path: {
      type: String,
      default: '',
    },
    actions: {
      type: Object,
      required: true,
    },
  },
  data: () => {
    return {
      popupVisibleFlg: false,
    }
  },
  methods: {
    /**
     * ポップアップを表示する
     */
    showPopup() {
      this.popupVisibleFlg = true
    },
    /**
     * ポップアップを非表示にする
     */
    hidePopup() {
      this.popupVisibleFlg = false
    },
    /**
     * 「左へ移動」ボタンクリックイベントハンドラ
     */
    handleClickMoveItemLeft() {
      this.hidePopup()
      this.actions.moveItemLeft(this.index)
    },
    /**
     * 「右へ移動」ボタンクリックイベントハンドラ
     */
    handleClickMoveItemRight() {
      this.hidePopup()
      this.actions.moveItemRight(this.index)
    },
    /**
     * 「画像を削除」ボタンクリックイベントハンドラ
     */
    handleClickDeleteItem() {
      this.hidePopup()
      this.actions.deleteItem(this.index)
    },
  },
}
</script>

<style lang="scss" scoped>
.c-image_card {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 100%;
  height: 100%;
  border: 1px solid #ccc;
  overflow: hidden;

  img {
    width: 100%;
  }

  &_setting {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 5px;
    right: 5px;
    width: 100px;
    height: 40px;
    background: rgba(0, 0, 0, 0.3);
    color: $COLOR_WHITE;
    cursor: pointer;
    user-select: none;
  }

  &_popup {
    position: absolute;
    top: 5px;
    right: 5px;
    padding: 10px;
    background: $COLOR_WHITE;
    box-shadow: -1px 1px 4px 0px $COLOR_BLACK;
    user-select: none;

    li + li {
      border-top: 1px solid #ccc;
    }

    &_button {
      display: block;
      position: relative;
      width: 100%;
      padding: 5px 5px 5px 25px;
      cursor: pointer;

      &:before {
        content: '';
        position: absolute;
        top: 50%;
        left: 0;
        width: 15px;
        height: 15px;
        background-size: contain;
        transform: translateY(-50%);
      }
      &.left:before {
        background-image: url(/images/common/ico_left.svg);
      }
      &.right:before {
        background-image: url(/images/common/ico_right.svg);
      }
      &.delete:before {
        background-image: url(/images/common/ico_trash.svg);
      }
      &.close:before {
        background-image: url(/images/common/ico_close.svg);
      }
    }
  }
}
</style>