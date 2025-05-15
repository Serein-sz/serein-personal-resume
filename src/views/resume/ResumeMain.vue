<script setup lang="ts">
import {
  ResizablePanelGroup,
  ResizablePanel,
  ResizableHandle,
} from '@/components/ui/resizable';
import LeftPanel from './LeftPanel.vue';
import RightPanel from './RightPanel.vue';
import html2canvas from 'html2canvas-pro';
import jsPDF from 'jspdf';
import Button from '@/components/ui/button/Button.vue';
import { ref } from 'vue';

const imageUrls = ref<string[]>([])

/**
 * 下载简历为PDF文件，支持多页导出
 * @author 王强
 * @date 2025-05-06
 * @version 1.0.0
 */
const downloadPdf = async () => {
  const resumeElement = document.getElementById('resume');
  if (resumeElement) {
    const originalHeight = resumeElement.style.height;
    resumeElement.style.height = `${resumeElement.scrollHeight}px`;

    try {
      // 确保样式应用并更新布局后再捕获
      await new Promise(resolve => setTimeout(resolve, 0));

      // 创建PDF文档
      const pdf = new jsPDF({
        orientation: 'portrait',
        unit: 'pt', // 使用点作为单位
        format: 'a4' // 使用标准A4尺寸
      });


      // 定义A4纸张尺寸（以像素为单位，基于72dpi）
      // A4纸张尺寸为210mm x 297mm
      const a4WidthPx = 595.28; // 210mm 转换为像素 (72dpi)
      const a4HeightPx = 841.89; // 297mm 转换为像素 (72dpi)

      const pageCount = Math.ceil(resumeElement.scrollHeight / a4HeightPx); // 计算总页数

      // 添加每一页到PDF
      for (let i = 0; i < pageCount; i++) {
        // 添加新页（第一页除外）
        if (i > 0) {
          pdf.addPage();
        }

        console.log(resumeElement)
        // 获取简历内容的画布
        const canvas = await html2canvas(resumeElement, {
          scale: 2, // 提高质量
          useCORS: true, // 处理跨域图片
          logging: true, // 启用日志调试
          windowHeight: a4HeightPx,
          height: a4HeightPx,
          y: a4HeightPx * i,
        });

        const imgData = canvas.toDataURL('image/png');
        imageUrls.value.push(imgData)

        console.log(canvas.height, canvas.width)
        console.log(a4HeightPx, a4WidthPx)

        // 将图像部分添加到PDF
        pdf.addImage(
          imgData,
          'PNG',
          0,
          0,
          a4WidthPx,
          a4HeightPx,
          undefined,
          'FAST',
        );
      }

      // 保存PDF文件
      pdf.save('resume.pdf');

    } catch (error) {
      console.error('导出PDF时发生错误:', error);
    } finally {
      resumeElement.style.height = originalHeight;
    }
  }
};


</script>
<template>
  <div class="w-screen overflow-y-scroll flex flex-col items-center p-12">
    <div class="flex mb-4">
      <Button @click="downloadPdf">下载简历 (PDF)</Button>
    </div>
    <img v-for="src in imageUrls" :src="src" class="mb-2" />
    <div id="resume" class="w-[794px]  border rounded-sm border-black flex font-sans">
      <ResizablePanelGroup id="demo-group-1" direction="horizontal">
        <ResizablePanel :default-size="30">
          <LeftPanel class="bg-black text-white h-full" />
        </ResizablePanel>
        <ResizableHandle />
        <ResizablePanel>
          <RightPanel class="h-full" />
        </ResizablePanel>
      </ResizablePanelGroup>
    </div>
  </div>
</template>
