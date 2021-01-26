<template>
  <div class="container">
    <h2 class="is-size-4 my-5">{{ msg }}</h2>
    <div class="field">
      <label class="label">R* = Скорость образования звезд</label>
      <div class="control">
        <input class="input is-primary" type="number" placeholder="Введите количество звёзд" v-model="R">
      </div>
    </div>
    <div class="field">
      <label class="label">f<sub>p</sub> =  Процент звезд с планетами</label>
      <div class="control">
        <input class="range" placeholder="Введите долю звёзд, обладающих планетами" type="range" min="0" step="1" max="100" v-model="Fp">
        <p>Текущее значение: <strong>{{ Fp }}%</strong></p>
      </div>
    </div>
    <div class="field">
      <label class="label">n<sub>e</sub> = Процент планет, способных поддерживать жизнь</label>
      <div class="control">
        <input class="input is-primary" type="number" placeholder="Введите значение" v-model="Ne">
      </div>
    </div>
    <div class="field">
      <div class="field-label">
        <label class="label">f<sub>l</sub> = Процент планет, способных поддерживать жизнь, на которых развивается жизнь</label>
      </div>
      <div class="field-bodyr my-3">
        <div class="field is-narrow ">
          <div class="control">
            <label class="radio">
              <input type="radio" name="member" id="one" value="1" checked v-model="picked">
                1 (Дрейк)
            </label>
            <label class="radio">
              <input type="radio" name="member" id="two" value="0.13" v-model="picked">
                0.13 (Лайнвивер)
            </label>
          </div>
          <span>Выбрано: {{ picked }}</span>
        </div>
      </div>
    </div>
    <div class="field">
      <label class="label">f<sub>i</sub> =  Вероятность возникновения разумных форм жизни на планете, на которой есть жизнь</label>
      <div class="control">
        <input class="input is-primary" type="text" placeholder="Введите значение"  v-model=" Fi">
      </div>
    </div>
    <div class="field">
      <label class="label">f<sub>c</sub> = Процент планет, на которых развивается разумная жизнь</label>
      <div class="control">
        <input class="range" placeholder="Введите значение" type="range" min="0" step="1" max="100" v-model="Fc">
        <p>Текущее значение: <strong>{{ Fc }}%</strong></p>
      </div>
    </div>
    <div class="field">
      <label class="label">L = Продолжительность жизни разумной цивилизации</label>
      <div class="control">
        <input class="input is-primary" type="text" placeholder="Введите значение"  v-model="L">
      </div>
    </div>
    <div class="field is-grouped my-4">
      <div class="control">
        <button class="button is-success" type="submit" v-on:click="calcResult(R,Fp,Ne,picked,Fi,Fc,L)">Рассчитать</button>
      </div>
      <div class="control">
        <button class="button is-warning" v-on:click="clear()">Отменить</button>
      </div>
    </div>
    <hr />
    <div class="field">
      <label class="label">N - количество разумных цивилизаций, готовых вступить в контакт</label>
      <div class="control">
        <div class="result-field is-success">
          Результат: {{ result || '' }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'calc',
  data() {
 return {
   result: 0,
   R:null,
   Fp:50,
   Ne:null,
   picked:1,
   Fi:null,
   Fc:50,
   L:null
 }
},
methods:{
  calcResult(R,Fp,Ne,picked,Fi,Fc,L) {
    this.result =  R*Fp*Ne*picked*Fi*Fc*L;
    return this.result;
  },
  clear() {
    this.result = 0,
    this.R = null,
    this.Fp =  50,
    this.Ne =  null,
    this.picked =  1,
    this.Fi =null,
    this.Fc =  50,
    this.L =  null
  }
},
  props: {
    msg: String
  }
}
</script>

<style lang="scss" scoped>
.container {
  border-radius: 4px;
  margin-top: 45px;
  width: 32%;
  padding:30px 20px;

  background: #fff;
  -webkit-box-shadow: 4px 4px 43px 0px rgba(0, 171, 5, 0.25);
  -moz-box-shadow: 4px 4px 43px 0px rgba(0, 171, 5, 0.25);
  box-shadow: 4px 4px 43px 0px rgba(0, 171, 5, 0.25);

  @media (max-width:1100px) {
    width: 40%;
  }
  @media (max-width:850px) {
    width: 60%;
  }
  @media (max-width:600px) {
    width: 80%;
  }
    @media (max-width:600px) {
    width: 100%;
    margin-top: 0;
    padding:35px 25px;
  }

  hr{
    background-color: #00d1b2;
  }

  .result-field{
    border: 1px solid #00d1b2;
    border-radius: 5px;
    padding-bottom: calc(.5em - 1px);
    padding-left: calc(.75em - 1px);
    padding-right: calc(.75em - 1px);
    padding-top: calc(.5em - 1px);
  }

  .range {
    width: 100%;
  }
}
</style>
