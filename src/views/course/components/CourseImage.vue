<template>
  <div class="course-image">
    <el-form-item :label="label">
      <el-upload
        class="avatar-uploader"
        action="https://jsonplaceholder.typicode.com/posts/"
        :show-file-list="false"
        :on-success="handleAvatarSuccess"
        :before-upload="beforeAvatarUpload"
        :http-request="handleUpload"
      >
        <!-- img 为预览图片的显示位置 -->
        <img v-if="value" :src="value" class="avatar">
        <i v-else class="el-icon-plus avatar-uploader-icon"></i>
      </el-upload>
    </el-form-item>
  </div>
</template>

<script>
import { uploadCourseImage } from '@/services/course'

export default {
  name: 'CourseImage',
  props: {
    value: {
      type: String
    },
    label: {
      type: String
    }
  },
  methods: {
    // 图片上传处理函数
    //   - option 为上传的相关信息
    //     - option.file 为上传的文件信息
    async handleUpload (option) {
      // 使用 FormData 对象处理
      const fd = new FormData()
      fd.append('file', option.file)
      // 发送上传请求
      const { data } = await uploadCourseImage(fd)
      if (data.code === '000000') {
        // data.data.name 服务端响应的，图片上传成功后的线上地址
        this.$emit('input', data.data.name)
      }
    },
    // 上传图片成功回调
    handleAvatarSuccess (res, file) {
      this.imageUrl = URL.createObjectURL(file.raw)
    },
    // 上传前的回调
    beforeAvatarUpload (file) {
      const isJPG = file.type === 'image/jpeg'
      const isLt2M = file.size / 1024 / 1024 < 2

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG 格式!')
      }
      if (!isLt2M) {
        this.$message.error('上传头像图片大小不能超过 2MB!')
      }
      return isJPG && isLt2M
    }
  }
}
</script>

<style lang="scss" scoped>
::v-deep .avatar-uploader .el-upload {
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
}
::v-deep .avatar-uploader .el-upload:hover {
  border-color: #409EFF;
}
.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  line-height: 178px;
  text-align: center;
}
.avatar {
  width: 178px;
  height: 178px;
  display: block;
}
</style>
