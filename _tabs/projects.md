---
layout: page
icon: fas fa-folder-open
order: 2
---

<style>
.project-container {
    display: grid;
    grid-template-columns: 1fr; /* 한 줄에 하나의 프로젝트 */
    gap: 20px;
    margin-bottom: 30px;
}

.project-card {
    border: 1px solid var(--border-color);
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    background-color: var(--card-bg);
    display: flex;
    flex-direction: row; /* 가로 정렬 */
    cursor: pointer;
}

.project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.project-image-container {
    width: 250px; /* 이미지 컨테이너 너비 고정 */
    /* height: 150px; */ /* 고정 높이 제거 */
    overflow: hidden;
    flex-shrink: 0; /* 컨테이너 크기 유지 */
}

.project-image {
    width: 100%;
    height: auto; /* 이미지 비율에 맞게 높이 자동 조정 */
    object-fit: cover; /* cover 유지, height:auto와 함께 사용시 문제 없음 */
    transition: transform 0.3s ease;
}

.project-card:hover .project-image {
    transform: scale(1.05);
}

.project-info {
    padding: 20px;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
}

.project-title {
    font-size: 1.5rem;
    margin: 0 0 10px 0;
    font-weight: 600;
    color: var(--link-color);
}

.project-description {
    color: var(--text-color);
    margin: 0 0 15px 0;
    font-size: 1rem;
    flex-grow: 1;
}

.project-tags {
    margin-top: auto;
    padding-top: 10px;
}

.project-tag {
    display: inline-block;
    background: var(--tag-bg);
    padding: 4px 12px;
    margin-right: 8px;
    margin-bottom: 8px;
    border-radius: 15px;
    font-size: 0.85rem;
    color: var(--tag-color);
    font-weight: 500;
}

.btn {
  display: inline-block;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  text-align: center;
  text-decoration: none;
  vertical-align: middle;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
  background-color: transparent;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  border-radius: 0.25rem;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.btn-primary {
  color: #fff;
  background-color: #0d6efd;
  border-color: #0d6efd;
}

.btn-primary:hover {
  color: #fff;
  background-color: #0b5ed7;
  border-color: #0a58ca;
}

/* 프로젝트 버튼을 키워드 태그 스타일로 변경 */
.project-button {
  display: inline-flex;
  align-items: center;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
  text-decoration: none;
  border: none;
  cursor: pointer;
  margin-right: 8px;
  margin-bottom: 8px;
  transition: all 0.3s ease;
}

.project-button:nth-child(1) {
  background-color: #e3f2fd;
  color: #1976d2;
}

.project-button:nth-child(2) {
  background-color: #f3e5f5;
  color: #7b1fa2;
}

.project-button:nth-child(3) {
  background-color: #e8f5e9;
  color: #2e7d32;
}

.project-button:nth-child(4) {
  background-color: #fff3e0;
  color: #f57c00;
}

.project-button:nth-child(5) {
  background-color: #fce4ec;
  color: #c2185b;
}

.project-button:nth-child(6) {
  background-color: #e0f7fa;
  color: #0097a7;
}

.project-button:nth-child(7) {
  background-color: #f1f8e9;
  color: #689f38;
}

.project-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* 라이트박스 스타일 */
.lightbox {
  display: none;
  position: fixed;
  z-index: 9999;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  cursor: pointer;
}

.lightbox-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 90%;
  max-height: 90%;
  cursor: default;
}

.lightbox-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.lightbox-close {
  position: absolute;
  top: 20px;
  right: 30px;
  color: white;
  font-size: 40px;
  font-weight: bold;
  cursor: pointer;
  z-index: 10000;
}

.lightbox-close:hover {
  color: #ccc;
}
</style>

<div class="project-container">
  {% assign sorted_projects = site.projects | sort: "start_date" | reverse %}
  {% for project in sorted_projects %}
    <div class="project-card">
      <div class="project-info">
        <h3 class="project-title">
          {{ project.title }}
        </h3>
        <p class="text-muted" style="font-size: 0.9rem; margin-bottom: 10px;">
          {% if project.start_date %}
            {{ project.start_date | date: "%Y-%m-%d" }} ~ {{ project.end_date | date: "%Y-%m-%d" }}
          {% else %}
            {{ project.date | date: "%B %d, %Y" }}
          {% endif %}
        </p>

        {% if project.buttons %}
        <div style="text-align: left; margin-bottom: 10px;">
          {% for button in project.buttons %}
          <button class="project-button" onclick="openLightbox('{{ site.baseurl }}{{ button.image }}', '{{ button.text }}')">{{ button.text }}</button>
          {% endfor %}
        </div>
        {% endif %}

        <p class="project-description">
          {{ project.description }}
        </p>
        {% if project.tags.size > 0 %}
        <div class="project-tags">
          {% for tag in project.tags %}
            <span class="project-tag">{{ tag }}</span>
          {% endfor %}
        </div>
        {% endif %}
      </div>
    </div>
  {% endfor %}
</div>

<!-- 라이트박스 HTML 구조 -->
<div id="lightbox" class="lightbox" onclick="closeLightbox()">
  <span class="lightbox-close" onclick="closeLightbox()">&times;</span>
  <div class="lightbox-content" onclick="event.stopPropagation()">
    <img id="lightbox-image" class="lightbox-image" src="" alt="" data-no-link="true">
  </div>
</div>

<script type="text/javascript">
function openLightbox(imageSrc, altText) {
  var lightbox = document.getElementById('lightbox');
  var lightboxImage = document.getElementById('lightbox-image');
  
  console.log('Loading image:', imageSrc);
  lightboxImage.src = imageSrc;
  lightboxImage.alt = altText;
  lightbox.style.display = 'block';
  
  lightboxImage.onerror = function() {
    console.error('Failed to load image:', imageSrc);
  };
  
  var escapeHandler = function(e) {
    if (e.key === 'Escape') {
      closeLightbox();
    }
  };
  document.addEventListener('keydown', escapeHandler);
  lightbox.escapeHandler = escapeHandler;
}

function closeLightbox() {
  var lightbox = document.getElementById('lightbox');
  lightbox.style.display = 'none';
  
  if (lightbox.escapeHandler) {
    document.removeEventListener('keydown', lightbox.escapeHandler);
    lightbox.escapeHandler = null;
  }
}
</script>
