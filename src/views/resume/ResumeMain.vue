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
import { Document, Packer, Paragraph, ImageRun } from 'docx';

const downloadPdf = async () => {
    const resumeElement = document.getElementById('resume');
    if (resumeElement) {
        const originalHeight = resumeElement.style.height;
        resumeElement.style.height = `${resumeElement.scrollHeight}px`;
        // Temporarily remove overflow hidden if it's set by parent or self, to ensure all content is visible
        // This might be necessary if the content itself has overflow properties that clip it.
        // However, the main issue is usually the container's fixed height.
        // resumeElement.style.overflow = 'visible'; 

        try {
            // Ensure styles are applied and layout is updated before capturing
            await new Promise(resolve => setTimeout(resolve, 0));

            const canvas = await html2canvas(resumeElement, {
                scale: 2, // Improve quality
                useCORS: true, // Handle cross-origin images if any
                logging: true, // Enable logging for debugging
                windowHeight: resumeElement.scrollHeight, // Ensure html2canvas 'sees' the full height
                height: resumeElement.scrollHeight // Set canvas height to full scroll height
            });
            const imgData = canvas.toDataURL('image/png');
            const pdf = new jsPDF({
                orientation: 'portrait',
                unit: 'px',
                format: [canvas.width, canvas.height] // Use canvas dimensions for PDF page size
            });
            pdf.addImage(imgData, 'PNG', 0, 0, canvas.width, canvas.height);
            pdf.save('resume.pdf');
        } catch (error) {
            console.error('Error generating PDF:', error);
            // Optionally, inform the user about the error
        } finally {
            resumeElement.style.height = originalHeight;
            // resumeElement.style.overflow = originalOverflow; // Restore original overflow
        }
    }
};

const downloadDocx = async () => {
    const resumeElement = document.getElementById('resume');
    if (resumeElement) {
        const originalHeight = resumeElement.style.height;
        resumeElement.style.height = `${resumeElement.scrollHeight}px`;

        try {
            await new Promise(resolve => setTimeout(resolve, 0));
            
            const canvas = await html2canvas(resumeElement, {
                scale: 2,
                useCORS: true,
                logging: true,
                windowHeight: resumeElement.scrollHeight,
                height: resumeElement.scrollHeight
            });
            
            const imgData = canvas.toDataURL('image/png');
            const doc = new Document({
                sections: [{
                    children: [
                        new Paragraph({
                            children: [
                                new ImageRun({
                                    data: imgData.split(',')[1],
                                    transformation: {
                                        width: canvas.width,
                                        height: canvas.height
                                    },
                                    type: 'png',
                                })
                            ]
                        })
                    ]
                }]
            });

            Packer.toBlob(doc).then((blob) => {
                const link = document.createElement('a');
                link.href = URL.createObjectURL(blob);
                link.download = 'resume.docx';
                link.click();
                URL.revokeObjectURL(link.href);
            });
        } catch (error) {
            console.error('Error generating DOCX:', error);
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
            <Button @click="downloadDocx" class="ml-2">下载简历 (DOCX)</Button>
        </div>
        <div id="resume" class="w-[794px] h-[1123px] border rounded-sm border-black flex font-sans">
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