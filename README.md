<index.html>
<html>
<head>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    .container { display: flex; }
    .terms, .definitions { width: 45%; margin: 10px; }
    .box { border: 1px solid #333; padding: 10px; margin: 5px; background: #f9f9f9; cursor: grab; }
    .dropzone { border: 2px dashed #999; padding: 10px; margin: 5px; min-height: 40px; }
    .correct { background: #c8f7c5; }
    .incorrect { background: #f7c5c5; }
  </style>
</head>
<body>

<h2> Drag-and-Drop: Match Medical Terms with Definitions</h2>
<p>Drag the correct definition to each medical term.</p>

<div class="container">
  <div class="terms">
    <div class="dropzone" data-answer="Chronic">Chronic</div>
    <div class="dropzone" data-answer="Diagnosis">Diagnosis</div>
    <div class="dropzone" data-answer="Prognosis">Prognosis</div>
    <div class="dropzone" data-answer="Inflammation">Inflammation</div>
    <div class="dropzone" data-answer="Hypertension">Hypertension</div>
    <div class="dropzone" data-answer="Anemia">Anemia</div>
    <div class="dropzone" data-answer="Antibiotic">Antibiotic</div>
    <div class="dropzone" data-answer="Benign">Benign</div>
    <div class="dropzone" data-answer="Malignant">Malignant</div>
    <div class="dropzone" data-answer="Vaccination">Vaccination</div>
    <div class="dropzone" data-answer="Rehabilitation">Rehabilitation</div>
    <div class="dropzone" data-answer="Contagious">Contagious</div>
  </div>

  <div class="definitions">
    <div class="box" draggable="true" data-term="Diagnosis">A medical conclusion identifying the nature of an illness or condition.</div>
    <div class="box" draggable="true" data-term="Prognosis">A prediction of the likely outcome of a disease or condition.</div>
    <div class="box" draggable="true" data-term="Inflammation">The body’s response to infection, injury, or irritation, often causing redness, heat, and swelling.</div>
    <div class="box" draggable="true" data-term="Hypertension">High blood pressure.</div>
    <div class="box" draggable="true" data-term="Anemia">A condition in which the blood has too few red blood cells or too little hemoglobin.</div>
    <div class="box" draggable="true" data-term="Antibiotic">A type of medicine that kills or slows the growth of bacteria.</div>
    <div class="box" draggable="true" data-term="Chronic">A long-lasting or recurring condition or illness.</div>
    <div class="box" draggable="true" data-term="Benign">An abnormal growth that is not cancerous.</div>
    <div class="box" draggable="true" data-term="Malignant">An abnormal growth that is cancerous and can spread to other parts of the body.</div>
    <div class="box" draggable="true" data-term="Vaccination">A substance or treatment that stimulates the body’s immune system to prevent disease.</div>
    <div class="box" draggable="true" data-term="Contagious">Able to spread from one person to another.</div>
    <div class="box" draggable="true" data-term="Rehabilitation">The process of restoring health through therapy after illness or injury.</div>
  </div>
</div>

<button onclick="checkAnswers()">Check Answers</button>

<script>
  const boxes = document.querySelectorAll('.box');
  const dropzones = document.querySelectorAll('.dropzone');

  boxes.forEach(box => {
    box.addEventListener('dragstart', e => {
      e.dataTransfer.setData('text/plain', box.dataset.term);
      e.dataTransfer.setData('text/html', box.outerHTML);
      setTimeout(() => box.style.display = "none", 0);
    });
    box.addEventListener('dragend', () => box.style.display = "block");
  });

  dropzones.forEach(zone => {
    zone.addEventListener('dragover', e => e.preventDefault());
    zone.addEventListener('drop', e => {
      e.preventDefault();
      const term = e.dataTransfer.getData('text/plain');
      const draggedBox = document.querySelector(`.box[data-term="${term}"]`);
      zone.innerHTML = `<strong>${zone.dataset.answer}</strong><br>${draggedBox.innerText}`;
      zone.dataset.dragged = term;
    });
  });

  function checkAnswers() {
    dropzones.forEach(zone => {
      if (zone.dataset.answer === zone.dataset.dragged) {
        zone.classList.add('correct');
        zone.classList.remove('incorrect');
      } else {
        zone.classList.add('incorrect');
        zone.classList.remove('correct');
      }
    });
  }
</script>

</body>
</html>
