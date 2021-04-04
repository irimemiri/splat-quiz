<template>
  <div id="app">
    <table>
      <tr>
        <th v-for="col in columns" :key="col">{{ col }}</th>
      </tr>
      <tr v-for="weapon in weapons" :key="weapon.id">
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
      columns: ['ID', 'ブキ', 'サブ', 'スペシャル'],
      weapons: [
        { id: 1, name: 'スプラシューター', subWeapon: 'スプラッシュボム', spWeapon: 'インクアーマー' },
        { id: 2, name: 'スプラローラー', subWeapon: 'カーリングボム', spWeapon: 'スーパーチャクチ' },
        { id: 3, name: 'スプラマニューバー', subWeapon: 'クイックボム', spWeapon: 'マルチミサイル' },
        { id: 4, name: 'パブロ', subWeapon: 'スプラッシュボム', spWeapon: 'スーパーチャクチ' },
        { id: 5, name: 'ボトルガイザー', subWeapon: 'スプラッシュボム', spWeapon: 'バブルランチャー' }
      ]
    }
  }
}
</script>

<style>
#app {
  /* for now */
  width: 600px;
  margin: 0 auto;
}
</style>
