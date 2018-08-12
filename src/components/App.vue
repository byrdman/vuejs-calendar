<template>
    <div>
        <div v-for="week in weeks">
            Week
            <div v-for="day in week">{{ day }}</div>
        </div>
    </div>
</template>
<script>
  export default {
    data() {
      return {
        month: 2,
        year: 2017
      };
    },
    computed: {
      days() {
        // Generating all days in current month
        let days = [];
        let currentDay = this.$moment(`${this.year}-${this.month}-1`, 'YYYY-M-D');

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
      },
      weeks() {
        let weeks = [];
        let week = [];

        for (let day of this.days) {
          week.push(day);
          if (week.length === 7) {
            weeks.push(week);
            week = [];
          }
        }
        return weeks;
      }
    }
  }
</script>