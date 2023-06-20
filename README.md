RobotDog
==

<template>
  <div>
    <div class="card" v-for="(card, index) in cards" :key="index" @click="selectCard(card)">
      <span>{{ card.name }}</span>
    </div>

    <div class="textbox" v-if="selectedCard">
      <el-dropdown>
        <span class="dropdown-trigger">
          <input type="text" v-model="selectedCardName" readonly @click="showDropdown">
        </span>
        <el-dropdown-menu v-if="showDropdownMenu">
          <el-dropdown-item v-for="option in selectedCard.options" :key="option" @click="selectOption(option)">{{ option }}</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>

<script>
import { Dropdown, DropdownMenu, DropdownItem } from 'element-ui';

export default {
  components: {
    ElDropdown: Dropdown,
    ElDropdownMenu: DropdownMenu,
    ElDropdownItem: DropdownItem
  },
  data() {
    return {
      cards: [
        { name: '1号卡片', options: ['A', 'C'] },
        { name: '2号卡片', options: ['X', 'Y'] },
        { name: '3号卡片', options: ['F', 'G'] },
        { name: '4号卡片', options: [] }
      ],
      selectedCard: null,
      selectedCardName: '',
      selectedOption: '',
      showDropdownMenu: false
    };
  },
  methods: {
    selectCard(card) {
      this.selectedCard = card;
      this.selectedCardName = card.name;
      this.selectedOption = '';
      this.showDropdownMenu = false;
    },
    showDropdown() {
      if (this.selectedCard && this.selectedCard.options.length > 0) {
        this.showDropdownMenu = true;
      }
    },
    selectOption(option) {
      this.selectedOption = option;
      this.showDropdownMenu = false;
    }
  }
};
</script>

<style>
.card {
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 10px;
  margin-bottom: 5px;
  background-color: lightgray;
}

.textbox {
  margin-top: 20px;
}

.dropdown-trigger {
  display: inline-block;
  cursor: pointer;
}

input[type="text"] {
  margin-right: 10px;
}
</style>
