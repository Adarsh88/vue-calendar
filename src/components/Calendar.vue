<template>
  <div class="mg-auto">
    <h1 class="text-4xl my-5 font-bold">Vue Calendar</h1>
    <section class="justify-center flex">
      <h2 class="text-2xl mt-10 font-bold">{{ currentMonthName }}-</h2>
      <h2 class="flex text-2xl mt-10 font-bold">{{ currentYear }}</h2>
    </section>
    <section class="flex mt-8 font-bold r">
      <p class="text-xl" style="width: 14.28%" v-for="day in days" :key="day">
        {{ day }}
      </p>
    </section>
    <section class="flex flex-wrap mt-3">
      <p
        class="mt-5"
        style="width: 14.28%"
        v-for="num in startDay()"
        :key="num"
      ></p>
      <p
        class="font-bold mt-5"
        style="width: 14.28%"
        v-for="num in daysInMonth()"
        :key="num"
        :class="currentDateClass(num)"
      >
        {{ num }}
      </p>
    </section>
    <section class="flex my-10 justify-evenly">
      <button class="px-2 border rounded font-bold" @click="back">
        Previous
      </button>
      <button class="px-2 border rounded font-bold" @click="next">Next</button>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: new Date().getDate(),
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
    };
  },
  methods: {
    daysInMonth() {
      // const month = new Date().getMonth() + 1;
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    startDay() {
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    },
    next() {
      if (this.currentMonth == 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    back() {
      if (this.currentMonth == 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    currentDateClass(num) {
      const calendatFullDate = new Date(
        this.currentYear,
        this.currentMonth,
        num
      ).toDateString();
      const currentFullDate = new Date().toDateString();
      return calendatFullDate === currentFullDate ? "text-green-500" : "";
      // num == currentDate ? "text-green-600 font-bold" : "";
    },
  },
  computed: {
    currentMonthName() {
      return new Date(this.currentYear, this.currentMonth).toLocaleString(
        "default",
        { month: "long" }
      );
    },
  },
};
</script>

<style></style>
