<template>

<div class="my-10">

  <div class="flex justify-center">
    <div>
      <p class="font-bold text-5xl">Résumé de course</p>
    </div>
  </div>

  <div class="flex justify-center">
    <p class="text-lg mt-3">Date 00/00/0000 à 00:00 </p>
  </div>

</div>


  <div class="flex flex-row place-content-around ms-20">
    <Ucard>
        <p class="my-5">Durée de la course : <span class="font-bold">value</span></p>
        <p class="my-5">Vitesse max : <span class="font-bold">value</span></p>
        <p class="my-5">Vitesse min : <span class="font-bold">value</span></p>
        <p class="my-5">Vitesse moyenne : <span class="font-bold">value</span></p>
    </Ucard>

    <canvas ref="lineChart" id="graphResume" class="max-w-xl max-h-60 " />

  </div>

  <div class="flex justify-center">
    <div class="my-10">
      <UButton color="sky" variant="soft" id="myExport" disabled>Save (export pdf à faire)</UButton>
    </div>
  </div>

</template>

<script>
  import Chart from 'chart.js/auto'

  (async function() {

    // try {
    //   // Fetching data from the API
    //   const response = await fetch('api/coursedata');
    //   const data = await response.json();
    const data = 
      [
        { duree: 10, vitesse: 5 },
        { duree: 20, vitesse: 13 },
        { duree: 30, vitesse: 11 },
        { duree: 40, vitesse: 18 },
        { duree: 48, vitesse: 18 },
      ];

    const maxDuree = Math.max(...data.map(row => row.duree));
    
    new Chart(
      document.getElementById('graphResume'),
      {
        type: 'line',
        data: {
          labels: data.map(row => row.duree),
          datasets: [
            { 
              label: 'Vitesse',
              data: data.map(row => row.vitesse),
              // data: data.map(row => ({x: row.duree, y: row.vitesse})),
              tension: 0.3 //courbure de la ligne
            }
          ]
        },
        options: {
          
          scales: {
            x: {
              title: {
                display: true,
                text: 'Durée (secondes)' // Optional: Label for x-axis
              },
              type: 'linear',
              max: maxDuree,
              ticks: {
                autoSkip: false, // Pour afficher toutes les étiquettes sans les ignorer
              },
              clip: false
            },
            y: {
              title: {
                display: true,
                text: 'Vitesse (unité)' // Optional: Label for y-axis
              },
              max: 30,
              beginAtZero: true
            }
          },
          
      }}
    );
  // } catch (error) {
  //     console.error('Error fetching the data:', error);
  //   }
  var downloadChartJs = () => {
    console.log('ca export')
    html2canvas(document.getElementById("graphResume"), {
      onrendered: function (canvas) {
        var img = canvas.toDataURL(); //image data of canvas
        var doc = new jsPDF();
        doc.addImage(img, 10, 10);
        doc.save('test.pdf');
      }
    });
  }
  document.getElementById("myExport").addEventListener("click", downloadChartJs);
    
  })();

</script>


<!-- 

a faire :
 
- Récupérer datas du back 
- Export pdf personnalisé
- plus de Custom ? Style/animations ?

Abde : 
- historique
- recevoir les infos quand course terminée

-->

