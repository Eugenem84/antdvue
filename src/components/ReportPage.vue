<template>
  <div class="report-page">
    <h2>Отчет по эффективности сотрудников</h2>

    <a-range-picker
        v-model:value="dateRange"
        format="YYYY-MM-DD"
        @change="onDateChange"
        style="margin-bottom: 20px"
    />

    <div style="margin-bottom: 20px">
      <a-input v-model:value="paramA" placeholder="Поиск по имени" style="width: 200px" />
      <a-input v-model:value="paramB" placeholder="Поиск по курению" style="width: 200px; margin-left: 20px" />
    </div>

    <a-table :columns="columns" :dataSource="filteredData" rowKey="id" />
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  name: "EmployeeReportPage",
  setup() {
    const data = ref([
      { id: 1, name: "Антон", modesty: 10, coffeeAmount: 5, smokeBreaks: 3, responseSpeed: "Молниеносно", date: "2024-12-01" },
      { id: 2, name: "Марина", modesty: 8, coffeeAmount: 3, smokeBreaks: 1, responseSpeed: "Минут 5", date: "2024-12-02" },
      { id: 3, name: "Ирина", modesty: 2, coffeeAmount: 7, smokeBreaks: 2, responseSpeed: "Через час", date: "2024-12-03" },
      { id: 4, name: "Сергей", modesty: 5, coffeeAmount: 6, smokeBreaks: 4, responseSpeed: "Два дня", date: "2024-12-04" },
      { id: 5, name: "Даша", modesty: 9, coffeeAmount: 4, smokeBreaks: 3, responseSpeed: "Отлично", date: "2024-12-05" },
      { id: 6, name: "Алексей", modesty: 4, coffeeAmount: 8, smokeBreaks: 5, responseSpeed: "Как получится", date: "2024-12-06" },
      { id: 7, name: "Оля", modesty: 7, coffeeAmount: 3, smokeBreaks: 2, responseSpeed: "Скоро", date: "2024-12-07" },
      { id: 8, name: "Никита", modesty: 6, coffeeAmount: 2, smokeBreaks: 4, responseSpeed: "Почти сразу", date: "2024-12-08" },
      { id: 9, name: "Ксения", modesty: 5, coffeeAmount: 4, smokeBreaks: 3, responseSpeed: "Не знаю", date: "2024-12-09" },
      { id: 10, name: "Дмитрий", modesty: 3, coffeeAmount: 6, smokeBreaks: 1, responseSpeed: "Минут 15", date: "2024-12-10" },
      { id: 11, name: "Екатерина", modesty: 9, coffeeAmount: 1, smokeBreaks: 0, responseSpeed: "Не спешу", date: "2024-12-11" },
      { id: 12, name: "Иван", modesty: 7, coffeeAmount: 7, smokeBreaks: 3, responseSpeed: "Сразу", date: "2024-12-12" },
      { id: 13, name: "Валерия", modesty: 4, coffeeAmount: 9, smokeBreaks: 5, responseSpeed: "Ближе к вечеру", date: "2024-12-13" },
      { id: 14, name: "Максим", modesty: 8, coffeeAmount: 4, smokeBreaks: 2, responseSpeed: "Когда получится", date: "2024-12-14" },
      { id: 15, name: "Татьяна", modesty: 6, coffeeAmount: 2, smokeBreaks: 3, responseSpeed: "Через пару часов", date: "2024-12-15" },
      { id: 16, name: "Петр", modesty: 3, coffeeAmount: 5, smokeBreaks: 1, responseSpeed: "До конца дня", date: "2024-12-16" },
      { id: 17, name: "Юлия", modesty: 10, coffeeAmount: 1, smokeBreaks: 0, responseSpeed: "Тут и сейчас", date: "2024-12-17" },
      { id: 18, name: "Роман", modesty: 2, coffeeAmount: 8, smokeBreaks: 4, responseSpeed: "Завтра утром", date: "2024-12-18" },
      { id: 19, name: "Мария", modesty: 6, coffeeAmount: 3, smokeBreaks: 2, responseSpeed: "Когда вспомню", date: "2024-12-19" },
      { id: 20, name: "Александра", modesty: 4, coffeeAmount: 4, smokeBreaks: 3, responseSpeed: "Не знаю, что будет", date: "2024-12-20" }
    ]);


    const dateRange = ref([]);
    const paramA = ref("");
    const paramB = ref(null);

    const onDateChange = (value) => {
      console.log(value);
    };

    const columns = [
      { title: "Дата", dataIndex: "date", key: "date" },
      { title: "Имя", dataIndex: "name", key: "name" },
      { title: "Скромность (1-10)", dataIndex: "modesty", key: "modesty" },
      { title: "Кофе в день (в чашках)", dataIndex: "coffeeAmount", key: "coffeeAmount" },
      { title: "Походы покурить", dataIndex: "smokeBreaks", key: "smokeBreaks" },
      { title: "Скорость реакции", dataIndex: "responseSpeed", key: "responseSpeed" }
    ];

    const filteredData = computed(() => {
      return data.value.filter((item) => {
        const isInDateRange =
            !dateRange.value[0] ||
            !dateRange.value[1] ||
            (new Date(item.date) >= new Date(dateRange.value[0]) &&
                new Date(item.date) <= new Date(dateRange.value[1]));

        const isNameMatch = item.name.toLowerCase().includes(paramA.value.toLowerCase());
        const isSmokeMatch = item.smokeBreaks >= (paramB.value ? parseInt(paramB.value) : 0);

        return isInDateRange && isNameMatch && isSmokeMatch;
      });
    });

    return {
      dateRange,
      paramA,
      paramB,
      columns,
      filteredData,
      onDateChange
    };
  }
};
</script>

<style scoped>
.report-page {
  padding: 20px;
}

a-input {
  margin-right: 20px;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

a-table {
  margin-top: 20px;
}
</style>
