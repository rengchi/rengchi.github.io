---
title: 'JQuery 方法'
date: 2025-03-04
tags: ['技术', 'js', 'jq']
---

# 拖动

```
(function ($) {
    $.fn.draggable = function () {
        var isDragging = false;
        var offsetX, offsetY;
        var $draggingElement;
        var isDragEvent = false; // 标记是否是拖动操作
        var dragThreshold = 5;   // 拖动的最小距离阈值，超过该距离就认为是拖动

        function savePosition(element, left, top) {
            document.cookie = `${element.attr('id')}_position=${left},${top};path=/`;
        }

        function loadPosition(element) {
            var cookies = document.cookie.split('; ');
            var elementId = element.attr('id');
            for (var i = 0; i < cookies.length; i++) {
                var parts = cookies[i].split('=');
                if (parts[0] === `${elementId}_position`) {
                    return parts[1].split(',').map(Number);
                }
            }
            return null;
        }

        this.each(function () {
            var $this = $(this);
            var position = loadPosition($this);
            if (position) {
                $this.css({
                    position: 'fixed',
                    left: position[0] + 'px',
                    top: position[1] + 'px'
                });
            } else {
                $this.css('position', 'fixed');
            }
        });

        this.on('mousedown', function (e) {
            $draggingElement = $(this);
            var originalPos = $draggingElement.offset();

            $draggingElement.css({
                left: originalPos.left + 'px',
                top: originalPos.top + 'px'
            });

            isDragging = true;
            offsetX = e.clientX - originalPos.left;
            offsetY = e.clientY - originalPos.top;
            isDragEvent = false; // 标记拖动开始
            e.preventDefault(); // 防止文本选择
        });

        $(document).on('mousemove', function (e) {
            if (isDragging) {
                var newLeft = e.clientX - offsetX;
                var newTop = e.clientY - offsetY;

                if (Math.abs(newLeft - $draggingElement.offset().left) > dragThreshold ||
                    Math.abs(newTop - $draggingElement.offset().top) > dragThreshold) {
                    isDragEvent = true;
                }

                $draggingElement.css({ left: newLeft + 'px', top: newTop + 'px' });
                savePosition($draggingElement, newLeft, newTop);
            }
        });

        $(document).on('mouseup', function () {
            isDragging = false;
        });

        this.on('click', function (e) {
            if (isDragEvent) {
                e.stopImmediatePropagation();
                return false;
            }
        });

        return this;
    };
})(jQuery);
```