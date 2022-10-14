<template>
  <div class="container">
    <div class="container__wrap">
      <div class="items-container items-changed">
        <a class="items-container__product"
           @click="changeItem(item)"
           v-for="item in activeUserItems"
           :key="item.id">{{item.name}}</a>
        <div class="count-items">selected: {{activeUserItems.length}}/6</div>
      </div>
      <div class="items-container">
        <a class="items-container__product"
           @click="changeItem(item)"
           v-for="item in userItems"
           :key="item.id">{{item.name}}</a>
      </div>
    </div>
    <div class="container__wrap">
      <div class="item-change">
        {{activeShopItem.name}}
      </div>
      <div class="items-container">
        <a class="items-container__product"
           v-for="item in shopItems"
           @click="changeShopItem(item)"
           :key="item.id">{{item.name}}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainComponent',
  data: () => ({
    activeUserItems: [],
    activeShopItem: {},
    userItems: [
      {
        "id": 1,
        "name": "Shoes 1"
      },
      {
        "id": 2,
        "name": "Shoes 2"
      },
      {
        "id": 3,
        "name": "Shoes 3"
      },
      {
        "id": 4,
        "name": "Shoes 4"
      },
      {
        "id": 5,
        "name": "T-shirt 1"
      },
      {
        "id": 6,
        "name": "T-shirt 2"
      },
      {
        "id": 7,
        "name": "T-shirt 3"
      },
      {
        "id": 8,
        "name": "T-shirt 4"
      }
    ],
    shopItems: [
      {
        "id": 11,
        "name": "Jacket 1"
      },
      {
        "id": 12,
        "name": "Jacket 2"
      },
      {
        "id": 13,
        "name": "Jacket 3"
      },
      {
        "id": 14,
        "name": "Jacket 4"
      },
      {
        "id": 15,
        "name": "Hoodie 1"
      },
      {
        "id": 16,
        "name": "Hoodie 2"
      },
      {
        "id": 17,
        "name": "Hoodie 3"
      },
      {
        "id": 18,
        "name": "Hoodie 4"
      }
    ]
  }),
  methods: {
    changeItem(item) {
      const includeItemId = this.activeUserItems.findIndex(el => el.id === item.id);
      if(includeItemId !== -1) {
        this.activeUserItems.splice(includeItemId, 1)
      } else {
        if(this.activeUserItems.length < 6) {
          this.activeUserItems.push(item)
        }
        else {
          this.activeUserItems.pop()
          this.activeUserItems.push(item)
        }
      }
    },
    changeShopItem(item) {
      if(this.activeShopItem.id === item.id) {
        this.activeShopItem = {}
      } else {
        this.activeShopItem = item
      }
    }
  }
}
</script>

<style scoped lang="scss">
.container {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  &__wrap {
    gap: 20px;
  }

  .items {
    &-container {
      display: grid;
      grid-auto-columns: 1fr;
      grid-auto-rows: 1fr;
      gap: 20px;
      box-sizing: border-box;
      border: 2px solid black;
      grid-template-columns: 1fr 1fr 1fr 1fr;
      grid-template-rows: auto;
      padding: 20px;
      min-height: 500px;

      &__product {
        width: 60px;
        height: 60px;
        padding: 20px;
        border: 2px solid black;
        font-size: 14px;
        cursor: pointer;
      }
    }

    &-changed {
      padding: 20px;
      width: 400px;
      min-height: 350px;
      margin-bottom: 20px;
      display: flex;
      justify-content: flex-start;
      flex-wrap: wrap;
    }
  }
  .item-change {
    width: 400px;
    min-height: 350px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 2px solid black;
    margin-left: auto;
    box-sizing: border-box;
    margin-bottom: 20px;
  }
  .count-items {
    margin-top: auto;
    width: 100%;
    text-align: center;
  }
}
</style>
