<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img :src="availableParts.heads[selectedIndices.head].src" title="head" />
        <button @click="selectNextPart('heads', 'down')" class="prev-selector">&#9668;</button>
        <button @click="selectNextPart('heads', 'up')" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="availableParts.arms[selectedIndices.leftArm].src" title="left arm" />
        <button @click="selectNextPart('leftArms', 'down')" class="prev-selector">&#9650;</button>
        <button @click="selectNextPart('leftArms', 'up')" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="availableParts.torsos[selectedIndices.torso].src" title="torso" />
        <button @click="selectNextPart('torsos', 'down')" class="prev-selector">&#9668;</button>
        <button @click="selectNextPart('torsos', 'up')" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="availableParts.arms[selectedIndices.rightArm].src" title="left arm" />
        <button @click="selectNextPart('rightArms', 'down')" class="prev-selector">&#9650;</button>
        <button @click="selectNextPart('rightArms', 'up')" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="availableParts.bases[selectedIndices.base].src" title="left arm" />
        <button @click="selectNextPart('bases', 'down')" class="prev-selector">&#9668;</button>
        <button @click="selectNextPart('bases', 'up')" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availableParts from '../data/parts';

export default {
  name: 'RobotBuilder',

  data() {
    return {
      availableParts,
      selectedPart: {},
      selectedIndices: {
        head: 0,
        torso: 0,
        rightArm: 0,
        leftArm: 0,
        base: 0,
      },

      selectedHeadIndex: 0,
      selectedTorsoIndex: 0,
      selectedRightArmIndex: 0,
      selectedLeftArmIndex: 0,
      selectedBaseIndex: 0,
    };
  },

  methods: {
    selectNextPart(type, direction) {
      switch (type) {
        case 'heads':
          this.selectedPart = { index: this.selectedIndices.head, parts: this.availableParts.heads };
          this.selectedIndices.head = this.applyPart(this.selectedPart, direction);
          break;
        case 'torsos':
          this.selectedPart = { index: this.selectedIndices.torso, parts: this.availableParts.torsos };
          this.selectedIndices.torso = this.applyPart(this.selectedPart, direction);
          break;
        case 'rightArms':
          this.selectedPart = { index: this.selectedIndices.rightArm, parts: this.availableParts.arms };
          this.selectedIndices.rightArm = this.applyPart(this.selectedPart, direction);
          break;
        case 'leftArms':
          this.selectedPart = { index: this.selectedIndices.leftArm, parts: this.availableParts.arms };
          this.selectedIndices.leftArm = this.applyPart(this.selectedPart, direction);
          break;
        case 'bases':
          this.selectedPart = { index: this.selectedIndices.base, parts: this.availableParts.bases };
          this.selectedIndices.base = this.applyPart(this.selectedPart, direction);
          break;
        default:
          break;
      }
    },
    applyPart(selectedPart, direction) {
      switch (direction) {
        case 'up':
          if (selectedPart.index + 1 < selectedPart.parts.length) {
            return selectedPart.index + 1;
          }
          return 0;
        case 'down':
          if (selectedPart.index > 0) {
            return selectedPart.index - 1;
          }
          return selectedPart.parts.length - 1;
        default:
          return 0;
      }
    },
  },
};
</script>

<style>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
</style>
