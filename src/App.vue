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
        <td>{{ weapon.sub }}</td>
        <td>{{ weapon.special }}</td>
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
        sub: 'サブ',
        special: 'スペシャル'
      },
      weapons: [
        { id: null, name: 'わかばシューター', sub: 'スプラッシュボム', special: 'インクアーマー' },
        { id: null, name: 'もみじシューター', sub: 'ロボットボム', special: 'アメフラシ' },
        { id: null, name: 'おちばシューター', sub: 'トーピード', special: 'バブルランチャー' },
        { id: null, name: 'スプラシューター', sub: 'クイックボム', special: 'スーパーチャクチ' },
        { id: null, name: 'スプラシューターコラボ', sub: 'スプラッシュボム', special: 'ジェットパック' },
        { id: null, name: 'スプラシューターベッチュー', sub: 'キューバンボム', special: 'マルチミサイル' },
        { id: null, name: 'プロモデラーMG', sub: 'キューバンボム', special: 'カーリングボムピッチャー' },
        { id: null, name: 'プロモデラーRG', sub: 'スプリンクラー', special: 'イカスフィア' },
        { id: null, name: 'プロモデラーPG', sub: 'クイックボム', special: 'ナイスダマ' },
        { id: null, name: 'N-ZAP85', sub: 'キューバンボム', special: 'インクアーマー' },
        { id: null, name: 'N-ZAP89', sub: 'ロボットボム', special: 'マルチミサイル' },
        { id: null, name: 'N-ZAP83', sub: 'スプリンクラー', special: 'アメフラシ' },
        { id: null, name: 'ボールドマーカー', sub: 'カーリングボム', special: 'スーパーチャクチ' },
        { id: null, name: 'ボールドマーカーネオ', sub: 'ジャンプビーコン', special: 'マルチミサイル' },
        { id: null, name: 'ボールドマーカー7', sub: 'スプラッシュボム', special: 'ウルトラハンコ' },
        { id: null, name: 'プライムシューター', sub: 'ポイントセンサー', special: 'アメフラシ' },
        { id: null, name: 'プライムシューターコラボ', sub: 'キューバンボム', special: 'バブルランチャー' },
        { id: null, name: 'プライムシューターベッチュー', sub: 'スプラッシュボム', special: 'ナイスダマ' },
        { id: null, name: '.52ガロン', sub: 'ポイントセンサー', special: 'イカスフィア' },
        { id: null, name: '.52ガロンデコ', sub: 'カーリングボム', special: 'ハイパープレッサー' },
        { id: null, name: '.52ガロンベッチュー', sub: 'スプラッシュシールド', special: 'ナイスダマ' },
        { id: null, name: '.96ガロン', sub: 'スプリンクラー', special: 'インクアーマー' },
        { id: null, name: '.96ガロンデコ', sub: 'スプラッシュシールド', special: 'スーパーチャクチ' },
        { id: null, name: 'シャープマーカー', sub: 'ポイズンミスト', special: 'ジェットパック' },
        { id: null, name: 'シャープマーカーネオ', sub: 'クイックボム', special: 'キューバンボムピッチャー' },
        { id: null, name: 'ジェットスイーパー', sub: 'ポイズンミスト', special: 'マルチミサイル' },
        { id: null, name: 'ジェットスイーパーカスタム', sub: 'クイックボム', special: 'ハイパープレッサー' },
        { id: null, name: 'L3リールガン', sub: 'カーリングボム', special: 'イカスフィア' },
        { id: null, name: 'L3リールガンD', sub: 'クイックボム', special: 'ジェットパック' },
        { id: null, name: 'L3リールガンベッチュー', sub: 'スプラッシュシールド', special: 'ウルトラハンコ' },
        { id: null, name: 'H3リールガン', sub: 'ポイントセンサー', special: 'マルチミサイル' },
        { id: null, name: 'H3リールガンD', sub: 'キューバンボム', special: 'インクアーマー' },
        { id: null, name: 'H3リールガンチェリー', sub: 'スプラッシュシールド', special: 'バブルランチャー' },
        { id: null, name: 'ボトルガイザー', sub: 'スプラッシュシールド', special: 'ハイパープレッサー' },
        { id: null, name: 'ボトルガイザーフォイル', sub: 'スプラッシュボム', special: 'バブルランチャー' },
        { id: null, name: 'スプラローラー', sub: 'カーリングボム', special: 'スーパーチャクチ' },
        { id: null, name: 'スプラローラーコラボ', sub: 'ジャンプビーコン', special: 'イカスフィア' },
        { id: null, name: 'スプラローラーベッチュー', sub: 'スプラッシュボム', special: 'バブルランチャー' },
        { id: null, name: 'カーボンローラー', sub: 'ロボットボム', special: 'アメフラシ' },
        { id: null, name: 'カーボンローラーデコ', sub: 'クイックボム', special: 'ロボボムピッチャー' },
        { id: null, name: 'ダイナモローラー', sub: 'トラップ', special: 'ハイパープレッサー' },
        { id: null, name: 'ダイナモローラーテスラ', sub: 'スプラッシュボム', special: 'インクアーマー' },
        { id: null, name: 'ダイナモローラーベッチュー', sub: 'スプリンクラー', special: 'ナイスダマ' },
        { id: null, name: 'ヴァリアブルローラー', sub: 'スプラッシュシールド', special: 'スプラッシュボムピッチャー' },
        { id: null, name: 'ヴァリアブルローラーフォイル', sub: 'キューバンボム', special: 'マルチミサイル' },
        { id: null, name: 'スプラマニューバー', sub: 'クイックボム', special: 'マルチミサイル' },
        { id: null, name: 'スプラマニューバーコラボ', sub: 'カーリングボム', special: 'ジェットパック' },
        { id: null, name: 'スプラマニューバーベッチュー', sub: 'キューバンボム', special: 'イカスフィア' },
        { id: null, name: 'デュアルスイーパー', sub: 'ポイントセンサー', special: 'マルチミサイル' },
        { id: null, name: 'デュアルスイーパー', sub: 'スプラッシュボム', special: 'アメフラシ' },
        { id: null, name: 'スパッタリー', sub: 'ジャンプビーコン', special: 'キューバンボムピッチャー' },
        { id: null, name: 'スパッタリーヒュー', sub: 'ポイズンミスト', special: 'アメフラシ' },
        { id: null, name: 'スパッタリークリア', sub: 'トーピード', special: 'スーパーチャクチ' },
        { id: null, name: 'ケルビン525', sub: 'トラップ', special: 'ジェットパック' },
        { id: null, name: 'ケルビン525デコ', sub: 'スプラッシュシールド', special: 'イカスフィア' },
        { id: null, name: 'ケルビン525ベッチュー', sub: 'タンサンボム', special: 'インクアーマー' },
        { id: null, name: 'クアッドホッパーブラック', sub: 'ロボットボム', special: 'スーパーチャクチ' },
        { id: null, name: 'クアッドホッパーホワイト', sub: 'スプリンクラー', special: 'ロボボムピッチャー' },
        { id: null, name: 'スプラチャージャー', sub: 'スプラッシュボム', special: 'ハイパープレッサー' },
        { id: null, name: 'スプラチャージャーコラボ', sub: 'スプラッシュシールド', special: 'キューバンボムピッチャー' },
        { id: null, name: 'スプラチャージャーベッチュー', sub: 'スプリンクラー', special: 'イカスフィア' },
        { id: null, name: 'スプラスコープ', sub: 'スプラッシュボム', special: 'ハイパープレッサー' },
        { id: null, name: 'スプラスコープコラボ', sub: 'スプラッシュシールド', special: 'キューバンボムピッチャー' },
        { id: null, name: 'スプラスコープベッチュー', sub: 'スプリンクラー', special: 'イカスフィア' },
        { id: null, name: 'スクイックリンα', sub: 'ポイントセンサー', special: 'インクアーマー' },
        { id: null, name: 'スクイックリンβ', sub: 'ロボットボム', special: 'イカスフィア' },
        { id: null, name: 'スクイックリンγ', sub: 'キューバンボム', special: 'ジェットパック' },
        { id: null, name: '14式竹筒銃・甲', sub: 'カーリングボム', special: 'マルチミサイル' },
        { id: null, name: '14式竹筒銃・乙', sub: 'ポイズンミスト', special: 'クイックボムピッチャー' },
        { id: null, name: '14式竹筒銃・丙', sub: 'タンサンボム', special: 'バブルランチャー' },
        { id: null, name: 'ソイチューバー', sub: 'キューバンボム', special: 'スーパーチャクチ' },
        { id: null, name: 'ソイチューバーカスタム', sub: 'カーリングボム', special: 'ジェットパック' },
        { id: null, name: 'リッター4K', sub: 'トラップ', special: 'アメフラシ' },
        { id: null, name: 'リッター4Kカスタム', sub: 'ジャンプビーコン', special: 'バブルランチャー' },
        { id: null, name: '4Kスコープ', sub: 'トラップ', special: 'アメフラシ' },
        { id: null, name: '4Kスコープカスタム', sub: 'ジャンプビーコン', special: 'バブルランチャー' },
        { id: null, name: 'ホットブラスター', sub: 'ポイズンミスト', special: 'スーパーチャクチ' },
        { id: null, name: 'ホットブラスターカスタム', sub: 'ロボットボム', special: 'ジェットパック' },
        { id: null, name: 'ロングブラスター', sub: 'キューバンボム', special: 'アメフラシ' },
        { id: null, name: 'ロングブラスターカスタム', sub: 'カーリングボム', special: 'バブルランチャー' },
        { id: null, name: 'ロングブラスターネクロ', sub: 'クイックボム', special: 'マルチミサイル' },
        { id: null, name: 'ノヴァブラスター', sub: 'スプラッシュボム', special: 'イカスフィア' },
        { id: null, name: 'ノヴァブラスターネオ', sub: 'トラップ', special: 'キューバンボムピッチャー' },
        { id: null, name: 'ノヴァブラスターベッチュー', sub: 'タンサンボム', special: 'アメフラシ' },
        { id: null, name: 'ラピッドブラスター', sub: 'トラップ', special: 'スプラッシュボムピッチャー' },
        { id: null, name: 'ラピッドブラスターデコ', sub: 'キューバンボム', special: 'ジェットパック' },
        { id: null, name: 'ラピッドブラスターベッチュー', sub: 'トーピード', special: 'イカスフィア' },
        { id: null, name: 'Rブラスターエリート', sub: 'ポイズンミスト', special: 'アメフラシ' },
        { id: null, name: 'Rブラスターエリートデコ', sub: 'スプラッシュシールド', special: 'インクアーマー' },
        { id: null, name: 'クラッシュブラスター', sub: 'スプラッシュボム', special: 'ハイパープレッサー' },
        { id: null, name: 'クラッシュブラスターネオ', sub: 'カーリングボム', special: 'マルチミサイル' },
        { id: null, name: 'バケットスロッシャー', sub: 'キューバンボム', special: 'マルチミサイル' },
        { id: null, name: 'バケットスロッシャーデコ', sub: 'スプリンクラー', special: 'イカスフィア' },
        { id: null, name: 'バケットスロッシャーソーダ', sub: 'スプラッシュボム', special: 'クイックボムピッチャー' },
        { id: null, name: 'オーバーフロッシャー', sub: 'スプラッシュシールド', special: 'アメフラシ' },
        { id: null, name: 'オーバーフロッシャーデコ', sub: 'スプリンクラー', special: 'キューバンボムピッチャー' },
        { id: null, name: 'スクリュースロッシャー', sub: 'ロボットボム', special: 'ハイパープレッサー' },
        { id: null, name: 'スクリュースロッシャーネオ', sub: 'ポイントセンサー', special: 'スプラッシュボムピッチャー' },
        { id: null, name: 'スクリュースロッシャーベッチュー', sub: 'タンサンボム', special: 'スーパーチャクチ' },
        { id: null, name: 'ヒッセン', sub: 'クイックボム', special: 'インクアーマー' },
        { id: null, name: 'ヒッセンヒュー', sub: 'スプラッシュボム', special: 'アメフラシ' },
        { id: null, name: 'エクスプロッシャー', sub: 'スプリンクラー', special: 'バブルランチャー' },
        { id: null, name: 'エクスプロッシャーカスタム', sub: 'ポイントセンサー', special: 'イカスフィア' },
        { id: null, name: 'スプラスピナー', sub: 'クイックボム', special: 'マルチミサイル' },
        { id: null, name: 'スプラスピナーコラボ', sub: 'カーリングボム', special: 'アメフラシ' },
        { id: null, name: 'スプラスピナーベッチュー', sub: 'ポイズンミスト', special: 'ウルトラハンコ' },
        { id: null, name: 'バレルスピナー', sub: 'スプリンクラー', special: 'ハイパープレッサー' },
        { id: null, name: 'バレルスピナーデコ', sub: 'スプラッシュシールド', special: 'バブルランチャー' },
        { id: null, name: 'バレルスピナーリミックス', sub: 'ポイントセンサー', special: 'ナイスダマ' },
        { id: null, name: 'クーゲルシュライバー', sub: 'ポイズンミスト', special: 'ジェットパック' },
        { id: null, name: 'クーゲルシュライバーヒュー', sub: 'ジャンプビーコン', special: 'アメフラシ' },
        { id: null, name: 'ノーチラス47', sub: 'ポイントセンサー', special: 'イカスフィア' },
        { id: null, name: 'ノーチラス79', sub: 'キューバンボム', special: 'ジェットパック' },
        { id: null, name: 'ハイドラント', sub: 'ロボットボム', special: 'スーパーチャクチ' },
        { id: null, name: 'ハイドラントカスタム', sub: 'トラップ', special: 'インクアーマー' },
        { id: null, name: 'パブロ', sub: 'スプラッシュボム', special: 'スーパーチャクチ' },
        { id: null, name: 'パブロヒュー', sub: 'トラップ', special: 'イカスフィア' },
        { id: null, name: 'パーマネントパブロ', sub: 'スプリンクラー', special: 'インクアーマー' },
        { id: null, name: 'ホクサイ', sub: 'ロボットボム', special: 'ジェットパック' },
        { id: null, name: 'ホクサイヒュー', sub: 'ジャンプビーコン', special: 'マルチミサイル' },
        { id: null, name: 'ホクサイベッチュー', sub: 'キューバンボム', special: 'ウルトラハンコ' },
        { id: null, name: 'パラシェルター', sub: 'スプリンクラー', special: 'アメフラシ' },
        { id: null, name: 'パラシェルターソレーラ', sub: 'ロボットボム', special: 'スプラッシュボムピッチャー' },
        { id: null, name: 'スパイガジェット', sub: 'トラップ', special: 'スーパーチャクチ' },
        { id: null, name: 'スパイガジェットソレーラ', sub: 'スプラッシュボム', special: 'イカスフィア' },
        { id: null, name: 'スパイガジェットベッチュー', sub: 'トーピード', special: 'インクアーマー' },
        { id: null, name: 'キャンピングシェルター', sub: 'ジャンプビーコン', special: 'バブルランチャー' },
        { id: null, name: 'キャンピングシェルターソレーラ', sub: 'スプラッシュシールド', special: 'カーリングボムピッチャー' },
        { id: null, name: 'キャンピングシェルターカーモ', sub: 'トラップ', special: 'ウルトラハンコ' },
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
  background-color: aliceblue;
  width: 800px;
  margin: 0 auto;
}

table {
  border-collapse: collapse;
}

th, td {
  border: solid 1px #fff;
  padding: 10px;
}

th {
  cursor: pointer;
}

th.sorted {
  background-color: skyblue;
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
