<template>
  <div class="background">
    <div class="workarea" ref="workarea">
      <div
        v-for="(object, key) in objects"
        class="moving"
        :key="key"
        :style="{ top: object[0] + 'px', left: object[1] + 'px' }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      borders: {
        top: 0,
        right: 0,
        bottom: 0,
        left: 0
      },
      moving: {
        width: 20,
        height: 20,
        cnt: 500
      },
      objects: []
    }
  },
  methods: {
    defineBorders () {
      this.dragArea = this.$refs.workarea;

      this.borders = {
        top: 0,
        right: this.dragArea.clientWidth - this.moving.width,
        bottom: this.dragArea.clientHeight - this.moving.height,
        left: 0
      }
    }
  },
  mounted () {
    this.defineBorders();

    for (let i = 0; i < this.moving.cnt; i++) {
      this.objects.push(
        [
          Math.round((this.borders.bottom - this.borders.top) * Math.random() + this.borders.top),
          Math.round((this.borders.right - this.borders.left) * Math.random() + this.borders.left),
        ]
      )
    }

    setInterval(() => {
      this.objects.forEach(el => {

        let variants = [];

        if (el[0] == this.borders.top && el[1] == this.borders.left) {
          variants = [2, 3, 4];
        }

        else if (el[0] == this.borders.top && el[1] == this.borders.right) {
          variants = [4, 5, 6];
        }

        else if (el[0] == this.borders.top) {
          variants = [2, 3, 4, 5, 6];
        }

        else if (el[0] == this.borders.bottom && el[1] == this.borders.left) {
          variants = [0, 1, 2];
        }

        else if (el[0] == this.borders.bottom && el[1] == this.borders.right) {
          variants = [0, 6, 7];
        }

        else if (el[0] == this.borders.bottom) {
          variants = [0, 1, 2, 6, 7];
        }

        else if (el[1] == this.borders.left) {
          variants = [0, 1, 2, 3, 4];
        }

        else if (el[1] == this.borders.right) {
          variants = [0, 4, 5, 6, 7];
        }

        else {
          variants = [0, 1, 2, 3, 4, 5, 6, 7];
        }

        let variant = variants[Math.floor(Math.random() * (variants.length + 1))]

        switch (variant) {
          case 0:
            --el[0];
            break;
          case 1:
            --el[0];
            ++el[1];
            break;
          case 2:
            ++el[1];
            break;
          case 3:
            ++el[0];
            ++el[1];
            break;
          case 4:
            ++el[0];
            break;
          case 5:
            ++el[0];
            --el[1];
            break;
          case 6:
            --el[1];
            break;
          case 7:
            --el[0];
            --el[1];
            break;
        }

      })
    }, 1);
  }
}
</script>

<style scoped>
.background {
  background-color: #e0a7fe;
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.workarea {
  background: rgb(78, 190, 255);
  background: -moz-linear-gradient(
    90deg,
    rgba(78, 190, 255, 1) 0%,
    rgba(132, 121, 254, 1) 100%
  );
  background: -webkit-linear-gradient(
    90deg,
    rgba(78, 190, 255, 1) 0%,
    rgba(132, 121, 254, 1) 100%
  );
  background: linear-gradient(
    90deg,
    rgba(78, 190, 255, 1) 0%,
    rgba(132, 121, 254, 1) 100%
  );
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#4ebeff",endColorstr="#8479fe",GradientType=1);
  width: 80vw;
  height: 80vh;
  position: relative;
}
.moving {
  background-image: url("./assets/element.png");
  background-size: contain;
  width: 20px;
  height: 20px;
  position: absolute;
  top: 0px;
  left: 0px;
  -webkit-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
  box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
}
</style>
