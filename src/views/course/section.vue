<template>
  <div class="course-section">
    课程内容管理
  </div>
</template>

<script>
export default {
  name: 'CourseSection',
  props: {
    courseId: {
      type: [String, Number],
      required: true
    }
  }
}
</script>

<style lang="scss" scoped></style>
