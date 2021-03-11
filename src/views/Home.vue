<template>
  <div class="frame">
    <div class="absoluteLineMiddle"></div>
    <div class="frame__number">
      HP {{ user.hp }} extraTop {{ extraTop }} extraBottom
      {{ extraBottom }} extraLeft: {{ extraLeft }} extraRIGHT:
      {{ extraRight }} spaceX:{{ marginLeft }} spaceY: {{ marginTop }} BoxX:{{
        user.box.rectX
      }}
      BoxY:{{ user.box.rectY }}
    </div>

    <Town v-if="town" :marginLeft="marginLeft" :marginTop="marginTop" />
    <Forest v-if="forest" :marginLeft="marginLeft" :marginTop="marginTop" />

    <div class="frame__outer">
      <svg class="frame__level">
        <circle
          class="progress-ring__circle"
          stroke="tomato"
          stroke-width="5"
          fill="transparent"
          r="50"
          cx="50"
          cy="50"
        />
      </svg>
      <div class="frame__outer__level">
        <div class="frame__outer__level__number">
          {{ user.level }}
        </div>
      </div>
    </div>

    <div
      id="characterFrame"
      :class="[
        characterSlot
          ? 'frame__character frame__displayBlock'
          : 'frame__character'
      ]"
    >
      <div class="frame__character__wrap">
        <button class="frame__character__wrap__button">Character</button>
        <button class="frame__character__wrap__button">Cultivation</button>
        <button
          class="frame__character__wrap__close"
          @click="characterSlot = false"
        >
          x
        </button>
      </div>
      <div class="frame__character__details">
        <div class="frame__character__details__items">
          <div class="frame__character__details__items__slot"></div>
          <div class="frame__character__details__items__slot"></div>
          <div class="frame__character__details__items__slot"></div>
          <div class="frame__character__details__items__slot"></div>
          <div class="frame__character__details__items__slot"></div>
        </div>
        <div class="frame__character__details__avatar">
          <div class="frame__character__details__avatar__name">
            REIN THE RULER
          </div>
          <div class="frame__character__details__avatar__level">
            Level {{ user.level }}
          </div>
          <div class="frame__character__details__avatar__exp">
            Exp {{ user.exp }}
          </div>

          <div class="frame__character__details__avatar__health">
            Hit Point: {{ user.hp }}
          </div>
          <div class="frame__character__details__avatar__mana">
            Mana: {{ user.mana }}
          </div>
          <div class="frame__character__details__avatar__attack">
            Attack: {{ user.attack }}
          </div>
          <div class="frame__character__details__avatar__defense">
            Defense: {{ user.defence }}
          </div>

          <div class="frame__character__details__avatar__rep">
            Reputation {{ user.reputation }}
          </div>
          <div class="frame__character__details__avatar__crime">
            Crime {{ user.crime }}
          </div>

          <div class="frame__character__details__avatar__strength">
            Strength {{ user.strengthPoint }}
          </div>
          <div class="frame__character__details__avatar__int">
            Intelligence {{ user.intelligentPoint }}
          </div>
          <div class="frame__character__details__avatar__obs">
            Defense {{ user.defencePoint }}
          </div>
          <div class="frame__character__details__avatar__hitpoint">
            Vitality {{ user.vitalityPoint }}
          </div>
          <div class="frame__character__details__avatar__extra">
            *Reduce {{ user.damageReduction }}% damage taken
          </div>
          <div class="frame__character__details__avatar__extra">
            *Health Recovery Rate {{ user.recoverHpRate }}
          </div>
          <div class="frame__character__details__avatar__extra">
            *Mana Recovery Rate {{ user.recoverMpRate }}
          </div>
        </div>
        <div class="frame__character__details__accessory">
          <div class="frame__character__details__accessory__slot"></div>
          <div class="frame__character__details__accessory__slot"></div>
          <div class="frame__character__details__accessory__slot"></div>
          <div class="frame__character__details__accessory__slot"></div>
        </div>
      </div>
    </div>

    <div
      id="skillFrame"
      :class="[
        skillSlot ? 'frame__skills frame__displayBlock' : 'frame__skills'
      ]"
    >
      <div class="frame__skills__title">
        <div class="frame__skills__title__text">SKILLS</div>
        <button class="frame__skills__title__close" @click="skillSlot = false">
          X
        </button>
      </div>
      <div class="frame__skills__wrap">
        <div class="frame__skills__wrap__column"></div>
        <div class="frame__skills__wrap__column"></div>
        <div class="frame__skills__wrap__column"></div>
      </div>
    </div>

    <div
      id="bagFrame"
      :class="[bagSlot ? 'frame__bag frame__displayBlock ' : 'frame__bag']"
    >
      <div class="frame__bag__title">
        <div class="frame__bag__title__text">Inventory</div>
        <div class="frame__bag__title__close" @click="bagSlot = false">X</div>
      </div>
      <div class="frame__bag__wrap">
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
        <div class="frame__bag__wrap__slot"></div>
      </div>
      <div class="frame__bag__resource">
        <div class="frame__bag__resource__space"></div>
        <div class="frame__bag__resource__money">
          <div class="frame__bag__resource__money__count">
            <i class="fas fa-gem"></i> 250
          </div>
        </div>
      </div>
    </div>

    <div class="frame__quest">
      <div class="frame__quest__title"><i class="fas fa-tasks"></i> Tasks</div>
      <div class="frame__quest__tasks">
        <div class="frame__quest__tasks__title">
          <i class="fas fa-question-circle"></i> Help the poor farmer
        </div>
        <div class="frame__quest__tasks__text">
          The poor farmer is getting harrased by the boar. Help the farmer by
          eliminate the bear around the area.
        </div>
        <div class="frame__quest__tasks__objective">
          <i class="fas fa-shield-alt"></i> Protect the farm for a full day
          cycle.
        </div>
      </div>
    </div>

    <div class="frame__userInfo">
      <div class="frame__userInfo__health__outer">
        <i class="fas fa-heart"></i>
        <div
          :style="{
            width: '100%',
            backgroundColor: 'crimson',
            position: 'absolute',
            bottom: '0',
            height: user.inlineStyleHP + '%'
          }"
        ></div>
      </div>

      <div class="frame__userInfo__mana__outer">
        <i class="fas fa-flask"></i>
        <div
          :style="{
            width: '100%',
            backgroundColor: 'rgb(65, 111, 211)',
            position: 'absolute',
            bottom: '0',
            height: user.inlineStyleMP + '%'
          }"
        ></div>
      </div>
    </div>

    <div class="frame__slots">
      <div class="frame__slots__left">
        <div class="frame__slots__left__hotBar"></div>
        <div class="frame__slots__left__hotBar"></div>
        <div class="frame__slots__left__hotBar"></div>
        <div class="frame__slots__left__hotBar"></div>
        <div class="frame__slots__left__hotBar"></div>
      </div>
      <div class="frame__slots__middle"></div>
      <div class="frame__slots__right">
        <div class="frame__slots__right__hotBar"></div>
        <div class="frame__slots__right__hotBar"></div>
        <div class="frame__slots__right__hotBar"></div>
        <div class="frame__slots__right__hotBar"></div>
        <div class="frame__slots__right__hotBar"></div>
      </div>
    </div>

    <div class="frame__functions">
      <div class="frame__functions__slots " id="characterButton"></div>
      <div class="frame__functions__slots" id="skillButton"></div>
      <div class="frame__functions__slots" id="bagButton"></div>
    </div>
  </div>
</template>

<script>
import { onMounted, reactive, toRefs } from "vue";
// @ is an alias to /src
import Town from "@/components/Town.vue";
import Forest from "@/components/Forest.vue";

export default {
  name: "Home",
  components: {
    Town,
    Forest
  },
  setup() {
    let state = reactive({
      user: {
        box: {
          rectX: 2090,
          rectY: 815,
          width: 70,
          height: 100
        },
        level: 1,
        totalExp: 60,
        exp: 0,
        maxExp: 100,
        hp: 100,
        maxHp: 100,
        mana: 50,
        maxMana: 50,
        attack: 10,
        defence: 50,
        reputation: 3,
        crime: 0,
        strengthPoint: 1,
        intelligentPoint: 1,
        defencePoint: 1,
        vitalityPoint: 1,
        recoverHpRate: 0.003,
        recoverMpRate: 0.3,
        damageReduction: 5,
        inlineStyleHP: null,
        inlineStyleMP: null
      },
      expLimit: [
        {
          level: 1,
          maxExp: 100
        },
        {
          level: 2,
          maxExp: 300
        },
        {
          level: 3,
          maxExp: 600
        },
        {
          level: 4,
          maxExp: 800
        },
        {
          level: 5,
          maxExp: 1000
        }
      ],
      town: false,
      forest: true,
      canvas: null,
      currentKey: null,
      leftClick: false,
      rightClick: false,
      upClick: false,
      downClick: false,
      playerSpeed: 500,
      lastTime: Date.now(),
      marginLeft: -1220,
      marginTop: -315,
      KeepTrackOfCharacterMovingRight: 0,
      characterSlot: true,
      skillSlot: false,
      bagSlot: false,
      extraRight: 0,
      extraLeft: 0,
      extraTop: 0,
      extraBottom: 0,
      fireAttack: false,
      clickLocation: [],
      attacks: [],
      attackSpeed: 20,
      monsterForest: [
        {
          id: "1",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 2200,
          positionY: 500,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "2",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 2300,
          positionY: 500,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "3",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 600,
          positionY: 700,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "4",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 650,
          positionY: 800,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "5",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 670,
          positionY: 900,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "6",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 600,
          positionY: 1500,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "7",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 700,
          positionY: 1500,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "8",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 650,
          positionY: 1600,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },

        {
          id: "11",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 900,
          positionY: 1200,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "12",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 1000,
          positionY: 1200,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "13",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 950,
          positionY: 1300,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "14",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 100,
          positionY: 1000,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "15",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 200,
          positionY: 1000,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "16",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 150,
          positionY: 1100,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "17",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3000,
          positionY: 1300,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "18",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3100,
          positionY: 1300,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "19",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3050,
          positionY: 1400,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "20",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3350,
          positionY: 800,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "21",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3450,
          positionY: 800,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "23",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3400,
          positionY: 900,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "24",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3800,
          positionY: 1100,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "25",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3800,
          positionY: 1200,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "26",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 3700,
          positionY: 1150,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "27",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 2800,
          positionY: 500,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "28",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 2900,
          positionY: 500,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "29",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 2250,
          positionY: 600,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "30",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 1550,
          positionY: 600,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "31",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 1450,
          positionY: 600,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        },
        {
          id: "32",
          name: "Slime",
          attackTrigger: false,
          timeDead: null,
          statusAlive: true,
          respawnTime: 15000,
          hp: 100,
          maxHp: 100,
          attack: 10,
          defense: 20,
          speed: 5,
          positionX: 1500,
          positionY: 700,
          width: 50,
          height: 50,
          attacks: [
            {
              id: "1",
              attack: 10,
              visualTrigger: false,
              skillTrigger: false,
              attackPositionX: null,
              attackPositionY: null,
              attackWidth: 25,
              attackHeight: 25,
              statusUsed: false,
              timeUsed: null,
              cooldown: 3000
            }
          ]
        }
      ]
    });
    let jsonState = localStorage.getItem("state");
    if (jsonState) {
      let extractJson = JSON.parse(jsonState);
      //console.log(extractJson);
      state = Object.assign(state, extractJson);
    }
    /*

    state.canvas.fillRect(2300, 500, 50, 50);
    state.canvas.fillRect(2200, 500, 50, 50);
    center: 2090, 815
    -1220, -315
        2080 -3616

      */

    window.addEventListener("beforeunload", function() {
      //localStorage.setItem("state", JSON.stringify(state));
    });

    onMounted(() => {
      //over write click event on these butotn
      document
        .querySelector("#characterButton")
        .addEventListener("click", function(e) {
          e.stopPropagation();
          state.characterSlot = !state.characterSlot;
          //console.log("skillButton:", state.characterSlot);
        });
      document
        .querySelector("#skillButton")
        .addEventListener("click", function(e) {
          e.stopPropagation();
          state.skillSlot = !state.skillSlot;
          //console.log("skillButton:", state.skillSlot);
        });
      document
        .querySelector("#bagButton")
        .addEventListener("click", function(e) {
          e.stopPropagation();
          state.bagSlot = !state.bagSlot;
          //console.log("bagButton", state.bagSlot);
        });

      //overwrite click on these ids
      document
        .querySelector("#characterFrame")
        .addEventListener("click", function(e) {
          e.stopPropagation();
          console.log("click inside these!");
        });
      document
        .querySelector("#skillFrame")
        .addEventListener("click", function(e) {
          e.stopPropagation();
          console.log("click inside these!");
        });
      document
        .querySelector("#bagFrame")
        .addEventListener("click", function(e) {
          e.stopPropagation();
          console.log("click inside these!");
        });
      //console.log("component is mounted!");
      //set our state to storage,
      var canvas = document.getElementById("myCanvas");
      state.canvas = canvas.getContext("2d");
      //console.log(state.canav);
      levelProgress();
      listenForKey();
      listenForKeyUp();
      listenForClick();
      window.requestAnimationFrame(gameLoop);
    });

    const caculateHpMP = () => {
      state.user.inlineStyleHP = (state.user.hp / state.user.maxHp) * 100;
      state.user.inlineStyleMP = (state.user.mana / state.user.maxMana) * 100;
    };

    const recoverRateHp = () => {
      //
      if (state.user.hp < state.user.maxHp) {
        if (state.user.hp + state.user.recoverHpRate < state.user.maxHp) {
          state.user.hp += state.user.recoverHpRate;
        } else if (
          state.user.hp + state.user.recoverHpRate >=
          state.user.maxHp
        ) {
          state.user.hp = state.user.maxHp;
        }
      }
    };

    const levelProgress = () => {
      var circle = document.querySelector("circle");
      var radius = circle.r.baseVal.value;
      var circumference = radius * 2 * Math.PI;

      circle.style.strokeDasharray = `${circumference} ${circumference}`;
      circle.style.strokeDashoffset = `${circumference}`;

      function setProgress(percent, maxPercent) {
        const offset = circumference - (percent / maxPercent) * circumference;
        circle.style.strokeDashoffset = offset;
      }

      setProgress(state.user.exp, state.user.maxExp);
    };

    //run this after kill monster
    const checkLevel = currentExp => {
      //check the current exp, check if it's more than the maxHP, if not, then leave it
      //if it's current exp - max exp and +1 to level
      //go to level limit and get the next level max exp in
      //check whatever exp you have left, if it's greater than or lesser than the right now max exp
      //if yes, repeat step,
      //if not then you are good, set whatever exp you have left as the current exp
      if (currentExp > state.user.maxExp) {
        state.user.exp = currentExp - state.user.maxExp;
        state.user.level += 1;
        levelProgress();
        //now get new maxExp for that level
        for (let i = 0; i < state.expLimit.length; i++) {
          //
          if (state.expLimit[i].level == state.user.level + 1) {
            state.user.maxExp = state.expLimit[i].maxExp;

            return checkLevel(state.user.exp);
          }
        }
      } else {
        levelProgress();
      }
    };

    const listenForKey = () => {
      document.addEventListener("keydown", function(e) {
        e.preventDefault();
        if (e.code == "ArrowLeft") {
          state.leftClick = true;
        } else if (e.code == "ArrowRight") {
          state.rightClick = true;
        } else if (e.code == "ArrowUp") {
          state.upClick = true;
        } else if (e.code == "ArrowDown") {
          state.downClick = true;
        }
      });
    };
    const listenForKeyUp = () => {
      document.addEventListener("keyup", function(e) {
        e.preventDefault();
        if (e.code == "ArrowLeft") {
          state.leftClick = false;
        } else if (e.code == "ArrowRight") {
          state.rightClick = false;
        } else if (e.code == "ArrowUp") {
          state.upClick = false;
        } else if (e.code == "ArrowDown") {
          state.downClick = false;
        }
      });
    };

    const listenForClick = () => {
      document.addEventListener("click", function(e) {
        if (e.button == 0) {
          //console.log(e.layerX, e.layerY);
          if (state.fireAttack == false) {
            state.fireAttack = true;
            state.clickLocation.push({
              id: "1",
              goX: Number(e.layerX),
              goY: Number(e.layerY)
            });
          }
        }
      });
    };

    const checkForAttack = () => {
      if (state.fireAttack) {
        //create an square to the left of character box
        //state.rectX, state.rectY
        //attack is 5/5, so state.rectX - 5, is the palce we place it and state.rectY is where we palce it
        //find the attack go to location
        for (let i = 0; i < state.clickLocation.length; i++) {
          state.attacks.push({
            id: "1",
            width: 20,
            height: 20,
            attackX: state.user.box.rectX - 20,
            attackY: state.user.box.rectY,
            goX: state.clickLocation[i].goX,
            goY: state.clickLocation[i].goY,
            xSign: null,
            YSign: null,
            xIteration: null,
            yIteration: null
          });
          state.fireAttack = false;
        }
        state.clickLocation = [];
      }
    };

    const drawAttack = () => {
      for (let i = 0; i < state.attacks.length; i++) {
        state.canvas.fillStyle = "black";
        state.canvas.fillRect(
          state.attacks[i].attackX,
          state.attacks[i].attackY,
          state.attacks[i].width,
          state.attacks[i].height
        );
      }
    };

    const checkForCollision = () => {
      //
      //go through each attack, check if it has any collision with monsters
      if (state.attacks.length > 0) {
        for (let i = 0; i < state.attacks.length; i++) {
          //now go through each monsters
          for (let j = 0; j < state.monsterForest.length; j++) {
            //check if the monster is alive before check collision
            if (state.monsterForest[j].statusAlive == true) {
              //now check for collision
              if (
                state.attacks[i].attackX <
                  state.monsterForest[j].positionX +
                    state.monsterForest[j].width &&
                state.attacks[i].attackX + state.attacks[i].width >
                  state.monsterForest[j].positionX &&
                state.attacks[i].attackY <
                  state.monsterForest[j].positionY +
                    state.monsterForest[j].height &&
                state.attacks[i].attackY + state.attacks[i].height >
                  state.monsterForest[j].positionY
              ) {
                //detected!
                if (state.monsterForest[j].hp - 10 <= 0) {
                  //if hp less than 0, set hp = 0, then say status alive false, and give a dead timer as right now
                  state.monsterForest[j].hp = 0;
                  state.monsterForest[j].statusAlive = false;
                  state.monsterForest[j].timeDead = Date.now();
                  state.attacks.splice(i, 1);
                  state.user.exp += 25;
                  state.user.totalExp += 25;
                  checkLevel(state.user.exp);
                  //go through monster skills and de trigger all of it
                  for (
                    let k = 0;
                    k < state.monsterForest[j].attacks.length;
                    k++
                  ) {
                    state.monsterForest[j].attackTrigger = false;
                    state.monsterForest[j].attacks[k].skillTrigger = false;
                    state.monsterForest[j].attacks[k].timeUsed = null;
                    state.monsterForest[j].attacks[k].statusUsed = false;
                    state.monsterForest[j].attacks[k].visualTrigger = false;
                  }
                  //if we hit something, then we break this attack loop, so we are not iterate over attack that no longer existed
                  break;
                } else {
                  state.monsterForest[j].attackTrigger = true;
                  state.monsterForest[j].hp -= 10;
                  state.attacks.splice(i, 1);
                  //if we hit something, then we break this attack loop, so we are not iterate over attack that no longer existed
                  break;
                }
              }
            }
          }
        }
      }
    };

    const updateAttack = () => {
      if (state.attacks.length > 0) {
        //find the place where it need to go
        //check x, and y : 2084, 634
        //location x,y: 2040, 815
        //x: 44, y:181
        //44/181 = 0.24, that's how many x should move while y move in 1
        for (let i = 0; i < state.attacks.length; i++) {
          if (state.attacks[i].XSign != null) {
            //check if the x and y are out of range, the specific attack attackX, attackY
            //if so have another fuction that scan attacks and delete all of the one out of range
            if (
              state.attacks[i].attackX >= -20 &&
              state.attacks[i].attackX <= 4000 &&
              state.attacks[i].attackY >= -20 &&
              state.attacks[i].attackY <= 3000
            ) {
              if (state.attacks[i].XSign == "-") {
                state.attacks[i].attackX =
                  state.attacks[i].attackX - state.attacks[i].xIteration;
              } else if (state.attacks[i].XSign == "+") {
                state.attacks[i].attackX =
                  state.attacks[i].attackX + state.attacks[i].xIteration;
              }

              if (state.attacks[i].YSign == "-") {
                state.attacks[i].attackY =
                  state.attacks[i].attackY - state.attacks[i].yIteration;
              } else if (state.attacks[i].YSign == "+") {
                state.attacks[i].attackY =
                  state.attacks[i].attackY + state.attacks[i].yIteration;
              }
            }
          } else {
            let resultX = state.attacks[i].attackX - state.attacks[i].goX;
            let resultY = state.attacks[i].attackY - state.attacks[i].goY;
            let valueIterationX = 0;
            let valueIterationY = 0;
            let xSign = "";
            let ySign = "";
            //determine - or  +
            if (resultX > 0) {
              xSign = "-";
            } else if (resultX < 0) {
              xSign = "+";
            } else {
              xSign = "nothing";
            }

            if (resultY > 0) {
              ySign = "-";
            } else if (resultY < 0) {
              ySign = "+";
            } else {
              ySign = "nothing";
            }

            if (Math.abs(resultX) > Math.abs(resultY)) {
              valueIterationY =
                Number(Math.abs(resultY / resultX).toFixed(2)) *
                state.attackSpeed;
              valueIterationX = 1 * state.attackSpeed;
            } else {
              valueIterationX =
                Number(Math.abs(resultX / resultY).toFixed(2)) *
                state.attackSpeed;
              valueIterationY = 1 * state.attackSpeed;
            }

            //now we go , we either - or +, and we know how many step we need to go for lower value
            /*console.log(
              resultX,
              resultY,
              valueIterationX,
              valueIterationY,
              xSign,
              ySign
            );*/
            //now update the attackLocation base on the sign and the values
            if (xSign == "-") {
              state.attacks[i].attackX =
                state.attacks[i].attackX - valueIterationX;
            } else if (xSign == "+") {
              state.attacks[i].attackX =
                state.attacks[i].attackX + valueIterationX;
            }

            if (ySign == "-") {
              state.attacks[i].attackY =
                state.attacks[i].attackY - valueIterationY;
            } else if (ySign == "+") {
              state.attacks[i].attackY =
                state.attacks[i].attackY + valueIterationY;
            }
            //update my state
            state.attacks[i].YSign = ySign;
            state.attacks[i].XSign = xSign;
            state.attacks[i].xIteration = valueIterationX;
            state.attacks[i].yIteration = valueIterationY;
          }
        }
      }
    };

    const drawTown = () => {
      state.canvas.clearRect(0, 0, 4000, 3000);
      /*road*/
      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(0, 1800, 4000, 250);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(700, 800, 250, 1700);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(2000, 800, 250, 2000);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(0, 800, 3600, 250);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(1600, 300, 250, 750);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(1600, 150, 950, 250);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(2400, 150, 250, 650);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(250, 0, 250, 800);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(2000, 0, 250, 300);

      state.canvas.fillStyle = "#ac762f";
      state.canvas.fillRect(3600, 0, 250, 1800);

      /*house & npc*/
      /*witch & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(150, 1250, 400, 400);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(300, 1680, 100, 100);

      /*merchant & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(1050, 1250, 400, 400);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(1200, 1680, 100, 100);

      /*school & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(1650, 1250, 200, 400);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(1880, 1450, 100, 100);

      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2300, 1250, 200, 400);

      /*farmer & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2750, 1450, 200, 200);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(2810, 1670, 100, 100);

      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2750, 1150, 500, 200);

      /*farmer & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(3350, 1550, 200, 200);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(3220, 1600, 100, 100);

      /*food store & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2350, 2250, 400, 200);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(2350, 2100, 100, 100);

      /*blacksmith & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2850, 2250, 400, 400);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(2980, 2100, 100, 100);

      /*fish vendor & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(1100, 2100, 300, 300);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(970, 2150, 100, 100);

      /*cook & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(1600, 2200, 300, 300);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(1700, 2070, 100, 100);

      /*clothes & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2800, 350, 500, 300);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(2900, 680, 100, 100);

      /*Alchemy & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(750, 350, 600, 300);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(1000, 680, 100, 100);

      /*Tower of the Fallen & npc*/
      state.canvas.fillStyle = "brown";
      state.canvas.fillRect(2000, 420, 250, 250);

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(2075, 690, 100, 100);

      /*haunt forest*/
      state.canvas.fillStyle = "orange";
      state.canvas.fillRect(325, 0, 100, 100);

      /*hunting forest*/
      state.canvas.fillStyle = "orange";
      state.canvas.fillRect(2075, 0, 100, 100);

      /*lake forest*/
      state.canvas.fillStyle = "orange";
      state.canvas.fillRect(3680, 0, 100, 100);

      /*ghost tree forest*/
      state.canvas.fillStyle = "orange";
      state.canvas.fillRect(775, 2400, 100, 100);

      /*farm tree forest*/
      state.canvas.fillStyle = "orange";
      state.canvas.fillRect(2075, 2700, 100, 100);

      /*Fences*/
      state.canvas.fillStyle = "red";
      state.canvas.fillRect(0, 750, 250, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(200, 0, 50, 750);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(500, 0, 50, 750);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(500, 750, 300, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1300, 750, 300, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1550, 150, 50, 600);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1550, 100, 450, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1950, 0, 50, 100);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2250, 0, 50, 100);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2250, 100, 450, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2650, 150, 50, 600);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2650, 750, 200, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3150, 750, 450, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3550, 0, 50, 750);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3850, 0, 50, 1750);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3850, 1750, 150, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3550, 1050, 50, 700);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3350, 1750, 250, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2300, 1050, 1250, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2250, 1050, 50, 200);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2250, 1650, 50, 100);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2250, 1750, 450, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1950, 1050, 50, 250);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1950, 1650, 50, 100);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1450, 1750, 550, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(950, 1750, 150, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(950, 1050, 50, 700);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1000, 1050, 950, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1000, 1050, 950, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(650, 1050, 50, 700);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(500, 1750, 200, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(0, 1750, 200, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(0, 1050, 50, 700);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(50, 1050, 600, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(0, 2050, 650, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(650, 2050, 50, 450);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(650, 2500, 300, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(950, 2300, 50, 250);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1450, 2050, 200, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1500, 2100, 50, 250);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1900, 2050, 50, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1950, 2050, 50, 750);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(1950, 2800, 350, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2250, 2250, 50, 550);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2550, 2050, 350, 50);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(2770, 2100, 50, 350);

      state.canvas.fillStyle = "red";
      state.canvas.fillRect(3300, 2050, 50, 350);

      /*character render*/
      state.canvas.fillStyle = "#ff8080";
      state.canvas.fillRect(
        state.user.box.rectX,
        state.user.box.rectY,
        state.user.box.width,
        state.user.box.height
      );
    };

    const drawForest = () => {
      state.canvas.clearRect(0, 0, 4000, 3000);

      state.canvas.beginPath();
      state.canvas.lineWidth = "5";
      state.canvas.fillStyle = "dodgerblue";
      state.canvas.strokeStyle = "dodgerblue";
      state.canvas.arc(505, 905, 150, 0, Math.PI * 2, true);
      state.canvas.fill();
      state.canvas.stroke();
      state.canvas.closePath();

      state.canvas.fillStyle = "green";
      state.canvas.fillRect(1850, 1000, 500, 500);

      state.canvas.beginPath();
      state.canvas.lineWidth = "5";
      state.canvas.fillStyle = "green";
      state.canvas.strokeStyle = "green";
      state.canvas.moveTo(2000, 3000);
      state.canvas.lineTo(2000, 2500);
      state.canvas.lineTo(1500, 2000);
      state.canvas.lineTo(1000, 2000);
      state.canvas.lineTo(0, 2400);
      state.canvas.lineTo(0, 3000);
      state.canvas.lineTo(2000, 3000);
      state.canvas.fill();
      state.canvas.stroke();
      state.canvas.closePath();

      state.canvas.beginPath();
      state.canvas.lineWidth = "5";
      state.canvas.fillStyle = "green";
      state.canvas.strokeStyle = "green";
      state.canvas.moveTo(2300, 3000);
      state.canvas.lineTo(2300, 2500);
      state.canvas.lineTo(2600, 2000);
      state.canvas.lineTo(4000, 2000);
      state.canvas.lineTo(4000, 3000);
      state.canvas.lineTo(2300, 3000);
      state.canvas.fill();
      state.canvas.stroke();
      state.canvas.closePath();

      state.canvas.beginPath();
      state.canvas.lineWidth = "5";
      state.canvas.fillStyle = "green";
      state.canvas.strokeStyle = "green";
      state.canvas.moveTo(1000, 0);
      state.canvas.lineTo(1300, 300);
      state.canvas.lineTo(3300, 300);
      state.canvas.lineTo(3600, 0);
      state.canvas.lineTo(1000, 0);
      state.canvas.fill();
      state.canvas.stroke();
      state.canvas.closePath();

      for (let i = 0; i < state.monsterForest.length; i++) {
        //make sure the statusAlive is true, so we know that we are only updating alive monster
        if (state.monsterForest[i].statusAlive == true) {
          state.canvas.fillStyle = "green";
          state.canvas.fillRect(
            state.monsterForest[i].positionX,
            state.monsterForest[i].positionY - 10,
            state.monsterForest[i].hp / (state.monsterForest[i].maxHp / 50),
            5
          );
          state.canvas.fillStyle = "blue";
          state.canvas.fillRect(
            state.monsterForest[i].positionX,
            state.monsterForest[i].positionY,
            state.monsterForest[i].width,
            state.monsterForest[i].height
          );
        }
      }

      /*character render*/
      state.canvas.fillStyle = "#ff8080";
      state.canvas.fillRect(
        state.user.box.rectX,
        state.user.box.rectY,
        state.user.box.width,
        state.user.box.height
      );
    };

    const update = dt => {
      if (state.leftClick) {
        let heyWeHitTheWall = false;
        /*check if marginLeft is 0 or - dt * slayerspeed make it less than 0*/
        if (state.extraRight > 0) {
          state.extraRight -= dt * state.playerSpeed;
          state.user.box.rectX -= dt * state.playerSpeed;
        } else {
          if (state.marginLeft + dt * state.playerSpeed >= 0) {
            state.marginLeft = 0;
            heyWeHitTheWall = true;
          } else {
            state.marginLeft += dt * state.playerSpeed;
          }

          if (state.user.box.rectX - dt * state.playerSpeed <= 0) {
            state.user.box.rectX = 0;
          } else {
            //if the wall hitted, now we record the extra step that we have to move left
            if (heyWeHitTheWall) {
              state.extraLeft += dt * state.playerSpeed;
              state.user.box.rectX -= dt * state.playerSpeed;
            } else {
              state.user.box.rectX -= dt * state.playerSpeed;
            }
          }
        }
      } else if (state.rightClick) {
        let heyWeHitTheWall = false;

        if (state.extraLeft > 0) {
          state.user.box.rectX += dt * state.playerSpeed;
          state.extraLeft -= dt * state.playerSpeed;
        } else {
          if (state.marginLeft - dt * state.playerSpeed <= -2080) {
            state.marginLeft = -2080;
            heyWeHitTheWall = true;
          } else {
            state.marginLeft -= dt * state.playerSpeed;
          }

          if (state.user.box.rectX + dt * state.playerSpeed >= 3900) {
            state.user.box.rectX = 3900;
          } else {
            if (heyWeHitTheWall) {
              state.extraRight += dt * state.playerSpeed;
              state.user.box.rectX += dt * state.playerSpeed;
            } else {
              state.user.box.rectX += dt * state.playerSpeed;
            }
          }
        }
      } else if (state.upClick) {
        let heyWeHitTheWall = false;
        if (state.extraBottom > 0) {
          state.user.box.rectY -= dt * state.playerSpeed;
          state.extraBottom -= dt * state.playerSpeed;
        } else {
          if (state.marginTop + dt * state.playerSpeed >= 0) {
            state.marginTop = 0;
            heyWeHitTheWall = true;
          } else {
            state.marginTop += dt * state.playerSpeed;
          }

          if (state.user.box.rectY - dt * state.playerSpeed <= 0) {
            state.user.box.rectY = 0;
          } else {
            if (heyWeHitTheWall) {
              state.extraTop += dt * state.playerSpeed;
              state.user.box.rectY -= dt * state.playerSpeed;
            } else {
              state.user.box.rectY -= dt * state.playerSpeed;
            }
          }
        }
      } else if (state.downClick) {
        let heyWeHitTheWall = false;
        if (state.extraTop > 0) {
          state.extraTop -= dt * state.playerSpeed;
          state.user.box.rectY += dt * state.playerSpeed;
        } else {
          if (state.marginTop - dt * state.playerSpeed <= -2030) {
            state.marginTop = -2030;
            heyWeHitTheWall = true;
          } else {
            state.marginTop -= dt * state.playerSpeed;
          }

          if (state.user.box.rectY + dt * state.playerSpeed >= 2900) {
            state.user.box.rectY = 2900;
          } else {
            if (heyWeHitTheWall) {
              state.user.box.rectY += dt * state.playerSpeed;
              state.extraBottom += dt * state.playerSpeed;
            } else {
              state.user.box.rectY += dt * state.playerSpeed;
            }
          }
        }
      }
    };

    const clearAttackHitBox = () => {
      //if the attack is outside of x: 0  or 4000, y: 0 or 3000, then clear it
      //if attack is complete, mean that it hit something, then clear it
      //first let's do if attack hit nothing and manage to get out side of the canvas range, clear it
      //let say, pretend the canvas range is x :0 and 3950, y: 0 and 2950
      if (state.attacks.length > 0) {
        for (let i = 0; i < state.attacks.length; i++) {
          if (state.attacks[i].attackX <= -20) {
            state.attacks.splice(i, 1);
          } else if (state.attacks[i].attackX >= 4000) {
            state.attacks.splice(i, 1);
          } else if (state.attacks[i].attackY <= -20) {
            state.attacks.splice(i, 1);
          } else if (state.attacks[i].attackY >= 3000) {
            state.attacks.splice(i, 1);
          }
        }
      }
    };

    const checkForRespawn = () => {
      for (let i = 0; i < state.monsterForest.length; i++) {
        let currentTime = Date.now();
        if (state.monsterForest[i].statusAlive == false) {
          if (
            currentTime - state.monsterForest[i].timeDead >=
            state.monsterForest[i].respawnTime
          ) {
            //reset
            state.monsterForest[i].statusAlive = true;
            state.monsterForest[i].timeDead = null;
            state.monsterForest[i].hp = state.monsterForest[i].maxHp;
          }
        }
      }
    };

    const checkForMonsterTrigger = () => {
      //go through each monster
      //if trigger find true, then the monster being attack, so it need to attack back
      //go through monster attack one by one, and check if attack on cooldown,
      //if attack not on cooldown
      //find user location and appear attack there, and then put attack on cooldown
      //if attack cooldown, check did it finish the cooldown
      //if it does, do the attack
      //if not, ignore
      for (let i = 0; i < state.monsterForest.length; i++) {
        if (state.monsterForest[i].attackTrigger == true) {
          //
          for (let j = 0; j < state.monsterForest[i].attacks.length; j++) {
            //
            if (state.monsterForest[i].attacks[j].statusUsed == true) {
              //skill is used
              //so we check cooldown
              let currentTime = Date.now();
              if (
                currentTime - state.monsterForest[i].attacks[j].timeUsed >=
                state.monsterForest[i].attacks[j].cooldown
              ) {
                //set trigger
                state.monsterForest[i].attacks[j].skillTrigger = true;
                state.monsterForest[i].attacks[j].timeUsed = Date.now();
                state.monsterForest[i].attacks[j].statusUsed = true;
                state.monsterForest[i].attacks[j].attackPositionX =
                  state.user.box.rectX + 27.5;
                state.monsterForest[i].attacks[j].attackPositionY =
                  state.user.box.rectY;
                state.monsterForest[i].attacks[j].visualTrigger = true;
              }
            } else {
              //set trigger
              state.monsterForest[i].attacks[j].skillTrigger = true;
              state.monsterForest[i].attacks[j].timeUsed = Date.now();
              state.monsterForest[i].attacks[j].statusUsed = true;
              state.monsterForest[i].attacks[j].visualTrigger = true;
              state.monsterForest[i].attacks[j].attackPositionX =
                state.user.box.rectX + 27.5;
              state.monsterForest[i].attacks[j].attackPositionY =
                state.user.box.rectY;
            }
          }
        }
      }
    };

    const checkForMonsterAttackDraw = () => {
      //go through attack, if it's trigger
      //check if the time it start using and right now is no less than 2 second
      //then display it
      //i fover 2 second, set trigger back to false
      //
      for (let i = 0; i < state.monsterForest.length; i++) {
        for (let j = 0; j < state.monsterForest[i].attacks.length; j++) {
          let currentTime = Date.now();
          if (
            state.monsterForest[i].statusAlive == true &&
            state.monsterForest[i].attacks[j].visualTrigger == true &&
            currentTime - state.monsterForest[i].attacks[j].timeUsed <= 300
          ) {
            //okay skill we can use
            //console.log("I am going to attack back 1");
            //we can use it, rectX rectY 70 100
            //get user location
            //appear an attack on user location
            //put attack on cooldown right now
            let attackPointX = state.user.box.rectX;
            let attackPointY = state.user.box.rectY;

            state.canvas.fillStyle = "black";
            state.canvas.fillRect(
              attackPointX,
              attackPointY,
              state.monsterForest[i].attacks[j].attackWidth,
              state.monsterForest[i].attacks[j].attackHeight
            );
          } else if (
            currentTime - state.monsterForest[i].attacks[j].timeUsed <=
            300
          ) {
            state.monsterForest[i].attacks[j].visualTrigger = false;
          }
        }
      }
    };

    const checkForMonsterAttackCollision = () => {
      //go through  monster attack, see if the skill trigger is on
      //find it position, if it hit character hitbox , do the damage and
      //dissappear it

      for (let i = 0; i < state.monsterForest.length; i++) {
        for (let j = 0; j < state.monsterForest[i].attacks.length; j++) {
          if (
            state.monsterForest[i].statusAlive == true &&
            state.monsterForest[i].attacks[j].skillTrigger == true &&
            state.monsterForest[i].attacks[j].statusUsed == true
          ) {
            //console.log("check for collision!3");
            //we want to do damage only 1 time in 1 cooldown
            //make sure it cooldown first then re use
            //now check for collision
            if (
              state.user.box.rectX <
                state.monsterForest[i].attacks[j].attackPositionX +
                  state.monsterForest[i].attacks[j].attackWidth &&
              state.user.box.rectX + state.user.box.width >
                state.monsterForest[i].attacks[j].attackPositionX &&
              state.user.box.rectY <
                state.monsterForest[i].attacks[j].attackPositionY +
                  state.monsterForest[i].attacks[j].attackHeight &&
              state.user.box.rectY + state.user.box.height >
                state.monsterForest[i].attacks[j].attackPositionY
            ) {
              //console.log("do - 5 damage");
              //detected
              if (state.user.hp > 0) {
                state.user.hp -= 5;
              }
              state.monsterForest[i].attacks[j].skillTrigger = false;
              break;
            }
          }
        }
      }
    };

    function gameLoop() {
      const currentTime = Date.now();
      const deltaTime = (currentTime - state.lastTime) / 1000;
      checkForRespawn();
      update(deltaTime);
      if (state.town) {
        drawTown();
      } else if (state.forest) {
        drawForest();
      }
      state.lastTime = currentTime;
      checkForAttack();
      drawAttack();
      checkForCollision();
      checkForMonsterTrigger();
      checkForMonsterAttackDraw();
      checkForMonsterAttackCollision();
      updateAttack();
      clearAttackHitBox();
      caculateHpMP();
      recoverRateHp();
      window.requestAnimationFrame(gameLoop);
    }

    //const clickSkillsButton = () => {}
    //const clickBagButton = () => {}

    return {
      ...toRefs(state),
      listenForKey
    };
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Vidaloka&display=swap");
#myCanvas {
  width: 4000px;
  height: 3000px;
  background-color: lightgrey;
}
.frame {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  position: relative;
  color: black;
}

.absoluteLineMiddle {
  position: fixed;
  width: 1px;
  height: 100vh;
  left: 50%;
}

.frame__number {
  position: absolute;
  top: 0;
  right: 0;
}

.frame__outer {
  position: fixed;
  width: 100px;
  height: 100px;
  top: 5px;
  left: 5px;
  border-radius: 50%;
}
.frame__level {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background-color: white;
}
.progress-ring__circle {
  transition: 0.35s stroke-dashoffset;
  transform: rotate(-90deg);
  transform-origin: 50% 50%;
}

.frame__outer__level {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 5px;
  border-radius: 50%;
}
.frame__outer__level__number {
  line-height: 100px;
  text-align: center;
  font-size: 3rem;
  cursor: context-menu;
  -webkit-user-select: none;
  color: orange;
  font-family: "Vidaloka", serif;
}
/*character*/
.frame__character {
  display: none;
  position: fixed;
  top: 150px;
  left: 150px;
  width: 340px;
  height: 540px;
  background-color: white;
  text-align: left;
}
.frame__character__wrap {
  width: 100%;
  height: 30px;
  background-color: lightgrey;
  display: flex;
  flex-flow: row nowrap;
  justify-content: flex-start;
}
.frame__character__wrap__button {
  width: 40%;
  height: 100%;

  font-size: 1rem;
  border: 0px;
}
.frame__character__wrap__close {
  width: 20%;
  height: 100%;

  font-size: 1rem;
  border: 0px;
}
.frame__character__wrap__close:hover {
  cursor: pointer;
}

.frame__character__wrap__button--bwhite {
  background-color: white;
}
.frame__character__wrap__button:focus,
.frame__character__wrap__close:focus {
  outline: 0px;
  background-color: white;
}
.frame__character__wrap__button:hover {
  cursor: pointer;
}

.frame__character__details {
  width: 100%;
  height: 510px;
  background-color: white;
  display: flex;
  flex-flow: row wrap;
}

.frame__character__details__items {
  width: 85px;
  height: 425px;
  background-color: rgb(51, 60, 63);
}
.frame__character__details__avatar {
  width: 255px;
  height: 425px;
}
.frame__character__details__accessory {
  width: 340px;
  height: 85px;
  background-color: rgb(51, 60, 63);
  display: flex;
  flex-flow: row nowrap;
}
.frame__character__details__items__slot {
  width: 85px;
  height: 85px;
  border: 1px solid white;
}
.frame__character__details__accessory__slot {
  width: 85px;
  height: 85px;
  border: 1px solid white;
}

.frame__character__details__avatar__name {
  font-size: 1.2rem;
  margin: 10px 10px;
}
.frame__character__details__avatar__level {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__exp {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__health {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__mana {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__attack {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__defense {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__rep {
  font-size: 1rem;
  margin: 15px 10px 0;
}
.frame__character__details__avatar__crime {
  font-size: 1rem;
  margin: 5px 10px 15px;
}
.frame__character__details__avatar__strength {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__int {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__obs {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__hitpoint {
  font-size: 0.95rem;
  margin: 5px 10px;
}
.frame__character__details__avatar__extra {
  font-size: 0.95rem;
  margin: 10px 10px 0;
}
/*health, mana*/
.frame__userInfo {
  width: 90px;
  height: 80px;
  position: fixed;
  left: 120px;
  bottom: 20px;
  display: flex;
}
.frame__userInfo__health__outer {
  width: 40px;
  height: 80px;
  background-color: rgb(88, 88, 88);
  border-radius: 20px;
  position: relative;
  overflow: hidden;
}

.frame__userInfo__mana__outer {
  margin-left: 10px;
  width: 40px;
  height: 80px;
  background-color: rgb(88, 88, 88);
  border-radius: 20px;
  position: relative;
  overflow: hidden;
}

.fa-flask {
  position: absolute;
  line-height: 80px;
  font-size: 25px;
  color: white;
  z-index: 99;
  margin-left: 50%;
  left: -11px;
}
.fa-heart {
  position: absolute;
  line-height: 80px;
  font-size: 25px;
  color: white;
  z-index: 99;
  margin-left: 50%;
  left: -12.5px;
}

/*Skills*/
.frame__skills {
  display: none;
  width: 900px;
  height: 540px;
  background-color: rgb(51, 60, 63);
  position: fixed;
  top: 150px;
  margin-left: 500px;
}
.frame__skills__title {
  width: 100%;
  height: 40px;
  color: white;
  text-align: left;
  line-height: 40px;
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
}
.frame__skills__title__text {
  width: 100px;
  height: 100%;
  text-align: center;
  background-color: rgb(51, 60, 63);
  color: white;
}

.frame__skills__title__close {
  width: 40px;
  height: 100%;
  text-align: center;
  background-color: rgb(51, 60, 63);
  color: white;
  border: 1px solid rgb(51, 60, 63);
}
.frame__skills__title__close:focus {
  background-color: white;
  outline: 0px;
  color: black;
  border: 1px solid white;
}
.frame__skills__title__close:hover {
  cursor: pointer;
}

.frame__skills__wrap {
  width: 900px;
  height: 500px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
.frame__skills__wrap__column {
  border: 1px solid white;
}

/*bag*/
.frame__bag {
  display: none;
  position: fixed;
  width: 400px;
  height: 640px;
  background-color: rgb(51, 60, 63);
  top: 150px;
  right: 0;
  z-index: 10;
}
.frame__bag__title {
  width: 100%;
  height: 40px;
  background-color: rgb(34, 39, 41);
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
}
.frame__bag__title__text {
  width: 90px;
  height: 100%;
  text-align: center;
  line-height: 40px;
  color: white;
}
.frame__bag__title__text:hover {
  cursor: pointer;
}
.frame__bag__title__close {
  width: 40px;
  height: 100%;
  background-color: grey;
  text-align: center;
  line-height: 40px;
  color: white;
}
.frame__bag__title__close:hover {
  cursor: pointer;
}

.frame__bag__wrap {
  width: 100%;
  height: 500px;
  overflow: auto;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 2px;
}
.frame__bag__wrap__slot {
  border: 1px solid white;
  height: 78px;
}
.frame__bag__wrap__slot:hover {
  cursor: pointer;
  background-color: rgba(243, 236, 236, 0.3);
}

.frame__bag__resource {
  width: 100%;
  height: 100px;
  background-color: rgb(34, 39, 41);
}
.frame__bag__resource__space {
  width: 100%;
  height: 40px;
}
.frame__bag__resource__money {
  width: 100%;
  height: 60px;
  text-align: left;
  color: white;
}

.frame__bag__resource__money__count {
  font-size: 1.7rem;
}
.fa-gem {
  line-height: 60px;
  font-size: 1.5rem;
  margin-left: 20px;
}

/*quest task*/
.frame__quest {
  position: fixed;
  width: 230px;
  border-left: 1px solid mediumseagreen;
  right: 5px;
  top: 200px;
  -webkit-user-select: none;
}
.frame__quest__title {
  width: 100%;
  height: 30px;
  background-color: mediumseagreen;
  color: white;
  line-height: 30px;
  text-align: left;
  font-size: 1.3rem;
  padding-left: 5px;
}
.fa-tasks {
  font-size: 1.25rem;
}
.frame__quest__tasks {
  width: 100%;
  height: 100%;
  text-align: left;
  padding: 5px 5px;
  background-color: rgba(255, 255, 255, 0.8);
}
.frame__quest__tasks__title {
  font-size: 1.2rem;
  color: black;
  color: crimson;
}
.frame__quest__tasks__text {
  font-size: 1rem;
  padding-bottom: 10px;
  padding: 5px 0px;
}

.frame__quest__tasks__objective {
  font-size: 1rem;
  padding-bottom: 10px;
  color: dodgerblue;
}

/*slots*/
.frame__slots {
  position: fixed;
  width: 1000px;
  height: 100px;
  bottom: 5px;
  left: -500px;
  margin-left: 50%;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
}
.frame__slots__left {
  width: 45%;
  height: 70px;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  border: 1px solid black;
}
.frame__slots__middle {
  width: 10%;
  height: 100px;
  background-color: rgb(100, 143, 100);
}
.frame__slots__right {
  width: 45%;
  height: 70px;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  border: 1px solid black;
}
.frame__slots__left__hotBar {
  border: 1px solid black;
  height: 68px;
  background-color: lightgrey;
}
.frame__slots__right__hotBar {
  border: 1px solid black;
  height: 68px;
  background-color: lightgrey;
}

/*functions*/
.frame__functions {
  position: fixed;
  width: 180px;
  height: 50px;
  bottom: 20px;
  right: 50px;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-around;
  align-items: center;
}
.frame__functions__slots {
  width: 50px;
  height: 50px;
  background-color: black;
}
.frame__functions__slots:hover {
  cursor: pointer;
}

.frame__displayBlock {
  display: block;
}
</style>
