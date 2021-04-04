<template>
  <div id="app">
    <p><label>ブキ名</label><input type="text" v-model="searchName"></p>
    <table>
      <tr>
        <th v-for="(col, key) in columns" :key="col" :class="sortedClass(key)" @click="switchSort(key)">
          {{ col }}
        </th>
      </tr>
      <tr v-for="weapon in limited" :key="weapon.id">
        <td>{{ weapon.id }}</td>
        <td>{{ weapon.name }}</td>
        <td>{{ weapon.subWeapon }}</td>
        <td>{{ weapon.spWeapon }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      limit: 20,
      sortKey: '',
      isAsc: true,
      searchName: '',
      columns: {
        id: 'ID',
        name: 'ブキ',
        subWeapon: 'サブ',
        spWeapon: 'スペシャル'
      },
      weapons: [
        { id: 1, name: 'スプラシューター', subWeapon: 'スプラッシュボム', spWeapon: 'インクアーマー' },
        { id: 2, name: 'スプラローラー', subWeapon: 'カーリングボム', spWeapon: 'スーパーチャクチ' },
        { id: 3, name: 'スプラマニューバー', subWeapon: 'クイックボム', spWeapon: 'マルチミサイル' },
        { id: 4, name: 'パブロ', subWeapon: 'スプラッシュボム', spWeapon: 'スーパーチャクチ' },
        { id: 5, name: 'ボトルガイザー', subWeapon: 'スプラッシュボム', spWeapon: 'バブルランチャー' }
      ],
      sortOrders() {
        let sortOrder = {}
        this.columns.forEach(key => sortOrder[key] = 1)
        return sortOrder
      }
    }
  },
  computed: {
    limited() {
      // return this.sorted.slice(0, this.limit)
      return this.sorted
    },
  　sorted() {
      const weapons = this.matched.slice()
      const order = this.isAsc ? 'asc' : 'desc'
      return _.orderBy(weapons, this.sortKey, order)
    },
    matched() {
      return this.weapons.filter(el => el.name.indexOf(this.searchName) > -1)
    }
  },
  methods: {
    switchSort(key) {
      if (this.sortKey === key) {
        this.isAsc = !this.isAsc
      } else {
        this.isAsc = true
        this.sortKey = key
      }
    },
    sortedClass(col) {
      let order = this.isAsc ? 'asc' : 'desc'
      return this.sortKey === col ? `sorted ${order}` : ''
    }
  }
}
</script>

<style>
#app {
  /* for now */
  width: 800px;
  margin: 0 auto;
}

table {
  border-collapse: collapse;
}

th, td {
  padding: 10px;
}

th {
  cursor: pointer;
}

th.sorted.asc::after {
    display: inline-block;
    content: '▲';
    font-size: .8em;
}

th.sorted.desc::after {
  display: inline-block;
  content: '▼';
  font-size: .8em;
}
</style>
