<template>
  <div class="card">
    <div class="rounded shadow-lg bg-white py-6 px-10">
      <div class="text-center text-xl font-bold text-sky-500">
        B M I 計 算 器
      </div>
      <form @submit.prevent="calculate">
        <label class="block text-slate-700 text-sm my-2" for="height">
          身高
        </label>
        <input
          class="shadow border-2 border-sky-500 rounded w-full py-2 px-3 text-gray-700 focus:outline-none focus:shadow-outline"
          id="height"
          name="height"
          type="text"
          v-model.number="height"
          placeholder="請輸入身高"
        />
        <label class="block text-slate-700 text-sm my-2" for="height">
          體重
        </label>
        <input
          class="shadow border-2 border-sky-500 rounded w-full py-2 px-3 text-gray-700 focus:outline-none focus:shadow-outline"
          id="weight"
          name="weight"
          type="text"
          v-model.number="weight"
          placeholder="請輸入體重"
        />
        <button
          type="submit"
          class="rounded-none w-full bg-sky-200 text-sky-600 text-md mt-8 p-2"
        >
          計算
        </button>
      </form>
      <div class="result my-4">
        <p class="text-sky-600 text-center text-lg">
          B M I = {{ bmi }} &nbsp;你的體重「{{ message }}」
        </p>
      </div>
      <div class="rangeBox">
        <div class="grid grid-cols-2 my-2 text-yellow-500">
          <p>過輕</p>
          <p>BMI &le; 18.5</p>
        </div>
        <div class="grid grid-cols-2 my-2 text-green-500">
          <p>正常</p>
          <p>BMI 18.5 &le; 24</p>
        </div>
        <div class="grid grid-cols-2 my-2 text-amber-500">
          <p>過重</p>
          <p>BMI 24 &le; 27</p>
        </div>
        <div class="grid grid-cols-2 my-2 text-orange-500">
          <p>輕度肥胖</p>
          <p>BMI 27 &le; 30</p>
        </div>
        <div class="grid grid-cols-2 my-2 text-rose-500">
          <p>中度肥胖</p>
          <p>BMI 30 &le; 35</p>
        </div>
        <div class="grid grid-cols-2 my-2 text-red-500">
          <p>重度肥胖</p>
          <p>BMI 35 &ge;</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "InputForm",
  props: {
    msg: String,
  },
  data() {
    return {
      height: 0,
      weight: 0,
      bmi: 0,
      message: "",
    };
  },
  computed: {
    formValid() {
      const { height, weight } = this;
      return +height > 0 && +weight > 0;
    },
  },
  methods: {
    calculate() {
      if (!this.formValid) {
        return;
      }
      const { height, weight } = this;
      let bmi = Math.round((weight / height ** 2) * 10000);
      switch (true) {
        case bmi >= 35:
          return (this.message = "重度肥胖"), (this.bmi = bmi);
        case bmi < 35 && bmi >= 30:
          return (this.message = "中度肥胖"), (this.bmi = bmi);
        case bmi < 30 && bmi >= 27:
          return (this.message = "輕度肥胖"), (this.bmi = bmi);
        case bmi < 27 && bmi >= 24:
          return (this.message = "過重"), (this.bmi = bmi);
        case bmi < 24 && bmi >= 18.5:
          return (this.message = "正常"), (this.bmi = bmi);
        default:
          return (this.message = "過輕"), (this.bmi = bmi);
      }
    },
  },
};
</script>

<style lang="postcss"></style>
