<template>
    <div>
        <div v-for="day in days">{{ day }}</div>
    </div>
</template>
<script>
  export default {
    data() {
      return {
        month: 5,
        year: 2017
      };
    },
    computed: {
      days() {
        // Generating all days in current month
        let days = [];
        let currentDay = this.$moment(`${this.year}-${this.month}-1`, 'YYYY-M-D');
        days.push(currentDay);
        do {
          days.push(currentDay);
          currentDay = this.$moment(currentDay).add(1, 'days');
        } while ((currentDay.month()+1) === this.month);

        // add previous days to start
        const SUNDAY = 0;
        const MONDAY = 1;
        currentDay = this.$moment(days[0]);
        while (currentDay.day() !== MONDAY) {
          currentDay = this.$moment(currentDay).subtract(1, 'days');
          days.unshift(currentDay);
        };

        // add extra days to end
        currentDay = this.$moment(days[days.length-1]);
        while (currentDay.day() !== SUNDAY) {
          currentDay = this.$moment(currentDay).add(1, 'days');
          days.push(currentDay);
        }

        return days;
      }
    }
  }
</script>