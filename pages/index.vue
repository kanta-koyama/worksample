<template>
  <div class="p-top">
    <div class="p-top_wrapper">
      <p class="p-top_upload">
        <label for="upload">ファイルを選択する</label>
        <input
          id="upload"
          ref="inputRef"
          type="file"
					accept="image/*"
          multiple
          @change="handleUpload"
        />
      </p>
      <ul class="p-top_items">
        <li v-for="(item, index) in items" :key="item.id" class="p-top_item">
          <IndexImageCard
            :index="index"
            :path="item.path"
            :actions="{
              moveItemLeft,
              moveItemRight,
              deleteItem,
            }"
          />
        </li>
      </ul>
      <p class="p-top_submit">
        <a
          :class="isEditedFlg ? '' : 'disabled'"
          href="javascript:void(0)"
          @click="updateItems"
          >保存</a
        >
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',
  data: () => {
    return {
      items: [],
      isEditedFlg: false,
    }
  },
  mounted() {
    this.fetchItems()
  },
  methods: {
    /**
     * 商品写真取得API
     */
    fetchItems() {
      axios
        .get('https://httpbin.org/get', {
          params: {
            user: 'USER_ID',
          },
        })
        .then((res) => {
          /**
           * APIレスポンスはユーザー情報を元に以下形式でデータを取得する想定
           * id: 画像ID
           * path: 画像のsrc属性
           */
          // this.items = res.data.args
          this.items = []
        })
    },
    /**
     * 商品写真更新API
     */
    updateItems() {
      if (!this.isEditedFlg) {
        return
      }

      axios.post('https://httpbin.org/post', this.items).then((res) => {
				this.isEditedFlg = false
        this.fetchItems()
      })
    },
    /**
     * 画像アップロードイベントハンドラ
     */
    handleUpload() {
      const { files } = this.$refs.inputRef

      for (let i = 0; i < files.length; i++) {
        const file = files[i]
        const reader = new FileReader()

        reader.onload = (e) => {
          this.items.push({
            id: `${file.name.replace('.', '_')}_${file.lastModified}`,
            path: e.target.result,
          })
        }
        reader.readAsDataURL(files[i])
      }

      this.isEditedFlg = true
    },
    /**
     * 画像を左へ移動するアクション
     */
    moveItemLeft(i) {
      if (this.items.length === 0 || i === 0) {
        return
      }
      const prevItem = this.items[i - 1]
      this.items[i - 1] = this.items[i]
      this.items[i] = prevItem
      this.$forceUpdate()
    },
    /**
     * 画像を右へ移動するアクション
     */
    moveItemRight(i) {
      if (this.items.length === 0 || i === this.items.length - 1) {
        return
      }
      const nextItem = this.items[i + 1]
      this.items[i + 1] = this.items[i]
      this.items[i] = nextItem
      this.$forceUpdate()
    },
    /**
     * 画像を一覧から削除するアクション
     */
    deleteItem(i) {
      this.items.splice(i)
    },
  },
}
</script>

<style lang="scss" scoped>
.p-top {
  padding: 20px 0;

  &_wrapper {
    margin: 0 auto;
    @include pc {
      width: $SCREEN_LG;
      padding: 0 12px;
    }
    @include sp {
      padding: 0 15px;
    }
  }

  &_upload {
    label {
      position: relative;
      padding: 5px 28px 5px 8px;
      border: 1px solid #ccc;
      cursor: pointer;

      &:after {
        content: '';
        position: absolute;
        top: 50%;
        right: 5px;
        width: 15px;
        height: 15px;
        background-image: url(/images/common/ico_upload.svg);
        background-size: contain;
        transform: translateY(-50%);
      }
    }
    input {
      display: none;
    }
  }

  &_items {
    display: flex;
    flex-wrap: wrap;
    margin-top: 30px;
    @include pc {
      margin-right: -20px;
      margin-bottom: -20px;
    }
    @include sp {
      margin-right: -10px;
      margin-bottom: -10px;
    }
  }

  &_item {
    @include pc {
      width: 235px;
      height: 235px;
      margin-right: 20px;
      margin-bottom: 20px;
    }
    @include sp {
      width: calc(50vw - 20px);
      height: calc(50vw - 20px);
      margin-right: 10px;
      margin-bottom: 10px;
    }

    img {
      width: 100%;
    }
  }

  &_submit {
    margin-top: 50px;
    text-align: center;

    a {
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto;
      height: 60px;
      background: #04d5ac;
      color: $COLOR_WHITE;
      font-size: $TEXT_XL;
      font-weight: $FONT_BOLD;
      @include pc {
        width: 500px;
      }
      @include sp {
        width: 100%;
      }

      &.disabled {
        opacity: 0.3;
      }
    }
  }
}
</style>
