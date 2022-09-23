<template>
  <div class="animation-container">
    {{ title }}
    <div class="hint">
      scroll to move
    </div>
    <div class="system-count">
      {{ Math.round(y * 0.3)}} earth days
    </div>
    <div class="system-container">
      <div v-for="planet in planets" :key="planet.name" class="orbit" :class="`orbit--${planet.name}`">
        <div class="planet" :class="`planet--${planet.name}`">
          <div class="planet__label" :class="`planet__label--${planet.name}`">
          </div>
        </div>
      </div>
      <div class="sun"></div>
    </div>
  </div>
</template>


<script setup>
import { ref, watch } from 'vue'
import gsap from 'gsap'
import { useWindowScroll  } from '@vueuse/core'

const title = ref("Solar system")
const { y } = useWindowScroll ()

const planets = ref([
  {
    name: "mercury",
    slowFactor: 1.2,
  },
  {
    name: "venus",
    slowFactor: 3,
  },
  {
    name: "earth",
    slowFactor: 5,
  },
  {
    name: "mars",
    slowFactor: 9.5,
  },
  {
    name: "jupiter",
    slowFactor: 60,
  },
  {
    name: "saturn",
    slowFactor: 145,
  },
  {
    name: "uranus",
    slowFactor: 420,
  },
  {
    name: "neptune",
    slowFactor: 825,
  },
])

watch(y, (newValue) => {
  if (newValue) {
    planets.value.forEach((planet) => {
      gsap.from(`.orbit--${planet.name}`, { rotate: newValue / planet.slowFactor * 1.5, duration: 1 })
      gsap.from(`.planet__label--${planet.name}`, { rotate: -(newValue / planet.slowFactor * 1.5), duration: 1 })
    })
  }
})

</script>

<style lang="css">
.hint {
  margin: 5px 0;
  font-size: 0.8rem;
  color: #483838;
}
.system-count {
  margin: 10px 0;
}
.animation-container {
  position: fixed;
}
.system-container {
  position: relative;
  width: min(88vw, 88vh);
  height: min(88vw, 88vh);
  border: 1px solid lightgray;
}
.orbit {
  position: absolute;
  border-radius: 50%;
  border: 1px solid rgba(0, 0, 0, 0.5);
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
}
.sun {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
  width: 8%;
  height: 8%;
  border-radius: 50%;
  background: #FD841F;
}
.planet {
  position: absolute;
  top: 0;
  border-radius: 50%;
  border: 2px solid #B7C4CF;
}
.planet__label {
  position: absolute;
  font-size: 0.5rem;
  color: #483838;

}
.planet--mercury {
  width: 10%;
  height: 10%;
  left: 20%;
  background: linear-gradient(0deg, rgba(194,172,141,1) 0%, rgba(228,223,186,1) 38%, rgba(228,223,186,1) 63%, rgba(194,172,141,1) 100%);;
}
.orbit--mercury {
  height: 15%;
  width: 15%;
}
.planet--venus {
  width: 12%;
  height: 12%;
  left: 20%;
  background: linear-gradient(0deg, rgba(214,132,17,1) 0%, rgba(236,225,139,1) 38%, rgba(236,225,139,1) 63%, rgba(214,132,17,1) 100%);
}
.orbit--venus {
  height: 25%;
  width: 25%;
}

.planet--earth {
  width: 12%;
  height: 12%;
  left: 16%;
  background: linear-gradient(0deg, rgba(34,118,195,1) 0%, rgba(0,212,63,1) 38%, rgba(0,212,63,0.9164040616246498) 63%, rgba(34,118,195,1) 100%);
}
.orbit--earth {
  height: 35%;
  width: 35%;
}

.planet--mars {
  width: 8%;
  height: 8%;
  left: 24%;
  background: linear-gradient(0deg, rgba(214,63,17,1) 0%, rgba(212,128,0,1) 38%, rgba(212,128,0,1) 63%, rgba(214,63,17,0.804359243697479) 100%);
}
.orbit--mars {
  height: 45%;
  width: 45%;
}

.planet--jupiter {
  width: 12%;
  height: 12%;
  left: 20%;
  background: linear-gradient(0deg, rgba(194,172,141,1) 0%, rgba(228,223,186,1) 21%, rgba(189,128,22,1) 31%, rgba(255,236,203,1) 47%, rgba(189,128,22,1) 61%, rgba(213,200,166,1) 75%, rgba(194,172,141,1) 100%);
}
.orbit--jupiter {
  height: 65%;
  width: 65%;
}

.planet--jupiter {
  width: 12%;
  height: 12%;
  left: 20%;
  background: linear-gradient(0deg, rgba(194,172,141,1) 0%, rgba(228,223,186,1) 21%, rgba(189,128,22,1) 31%, rgba(255,236,203,1) 47%, rgba(189,128,22,1) 61%, rgba(213,200,166,1) 75%, rgba(194,172,141,1) 100%);
}
.orbit--jupiter {
  height: 60%;
  width: 60%;
}

.planet--saturn {
  width: 6%;
  height: 6%;
  left: 26%;
  background: linear-gradient(0deg, rgba(194,194,141,1) 0%, rgba(241,228,106,1) 47%, rgba(194,172,141,1) 100%);
}

.planet--saturn::after {
    content: "";
    width: 220%;
    height: 0px;
    border-top: 4px solid #E6B325;
    border-radius: 20%;
    position: absolute;
    top: 40%;
    left: -60%;
}

.orbit--saturn {
  height: 75%;
  width: 75%;
}


.planet--uranus {
  width: 4%;
  height: 4%;
  left: 32%;
  background: linear-gradient(0deg, rgba(141,194,187,1) 0%, rgba(165,244,233,1) 47%, rgba(141,194,187,1) 100%);
}

.orbit--uranus {
  height: 88%;
  width: 88%;
}

.planet--neptune {
  width: 4%;
  height: 4%;
  left: 32%;
  background: linear-gradient(0deg, rgba(33,187,186,1) 0%, rgba(17,90,189,1) 47%, rgba(33,187,186,1) 100%);
}

.orbit--neptune {
  height: 98%;
  width: 98%;
}



</style>