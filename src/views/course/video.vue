<template>
  <div class="course-video">
    <el-card>
      <div slot="header">
        课程相关信息
      </div>
      <el-form>
        <el-form-item label="视频上传">
          <input type="file">
        </el-form-item>
        <el-form-item label="封面上传">
          <input type="file">
        </el-form-item>
        <el-form-item>
          <el-button type="primary">开始上传</el-button>
          <el-button
            @click="$router.push({
              name: 'course-section',
              params: {
                courseId
              }
            })"
          >返回</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'CourseVideo',
  props: {
    courseId: {
      type: [String, Number],
      required: true
    }
  }
}
</script>

<style lang="scss" scoped></style>
