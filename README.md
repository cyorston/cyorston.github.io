# Hi, I'm Cole Yorston

Welcome to my portfolio!  
I'm a Lead Test Engineer working on advanced data acquisition and analytical methods for next-generation gas turbine systems, combining hands-on engineering with data-driven problem solving. 
Explore below for my background and projects I am working on.

---

## 🎓 & 💼 Interactive Career Timeline

<div id="timeline"></div>

---

## 🧠 Interactive Skills Network

<div id="skills"></div>

---

<script src="https://d3js.org/d3.v7.min.js"></script>
<script>
// ========================================
// D3 VERTICAL CAREER TIMELINE (Dark Mode)
// ========================================

const data = [
  {
    year: "2017–2021",
    title: "B.S. in Mechanical Engineering, University of Georgia",
    logo: "assets/img/uga.png",
    description: "Focused on IoT systems, signal processing, and early machine learning applications for real-time data pipelines."
  },
  {
    year: "2021–2023",
    title: "Graduate Research Assistant, University of Georgia",
    logo: "assets/img/uga_research.png",
    description: "Developed cloud-based monitoring solutions with ML classifiers for predictive maintenance; co-authored two publications."
  },
  {
    year: "2023–2024",
    title: "Test Engineer, Textron Specialized Vehicles",
    logo: "assets/img/tsv.png",
    description: "Implemented anomaly detection workflows to streamline validation and improve data quality processes."
  },
  {
    year: "2024–Present",
    title: "Data Scientist, Textron Specialized Vehicles",
    logo: "assets/img/tsv_ds.png",
    description: "Leading analytical initiatives to improve quality, develop ML models, and automate ETL pipelines for enterprise analytics."
  }
];

const width = 700;
const nodeHeight = 160;
const margin = { top: 40, right: 40, bottom: 40, left: 40 };
const height = data.length * nodeHeight + margin.top + margin.bottom;

const svgTimeline = d3.select("#timeline")
  .append("svg")
  .attr("width", "100%")
  .attr("height", height)
  .style("background", "#0d1117")
  .style("color", "#c9d1d9")
  .style("border-radius", "10px");

svgTimeline.append("line")
  .attr("x1", width / 2)
  .attr("y1", margin.top)
  .attr("x2", width / 2)
  .attr("y2", height - margin.bottom)
  .attr("stroke", "#58a6ff")
  .attr("stroke-width", 3)
  .attr("stroke-linecap", "round");

const nodeGroup = svgTimeline.selectAll(".node")
  .data(data)
  .enter()
  .append("g")
  .attr("class", "node")
  .attr("transform", (d, i) => `translate(${width / 2}, ${margin.top + i * nodeHeight})`);

nodeGroup.append("circle")
  .attr("r", 10)
  .attr("fill", "#58a6ff")
  .attr("stroke", "#1f6feb")
  .attr("stroke-width", 2);

nodeGroup.append("image")
  .attr("xlink:href", d => d.logo)
  .attr("x", -25)
  .attr("y", -70)
  .attr("width", 50)
  .attr("height", 50)
  .attr("clip-path", "circle(25px at center)");

nodeGroup.append("text")
  .attr("x", -40)
  .attr("y", -30)
  .attr("text-anchor", "end")
  .attr("fill", "#c9d1d9")
  .style("font-size", "13px")
  .style("font-weight", "600")
  .text(d => d.year);

nodeGroup.append("foreignObject")
  .attr("x", 30)
  .attr("y", -60)
  .attr("width", 320)
  .attr("height", 120)
  .html(d => `
    <div xmlns="http://www.w3.org/1999/xhtml" style="color:#c9d1d9;">
      <strong style="color:#58a6ff;">${d.title}</strong><br/>
      <p style="margin-top:5px;font-size:13px;">${d.description}</p>
    </div>
  `);

nodeGroup.on("mouseover", function() {
  d3.select(this).select("circle")
    .transition().duration(200)
    .attr("fill", "#1f6feb");
})
.on("mouseout", function() {
  d3.select(this).select("circle")
    .transition().duration(200)
    .attr("fill", "#58a6ff");
});


// ========================================
// D3 FORCE-DIRECTED SKILLS GRAPH (Dark Mode + Icons)
// ========================================

const skills = {
  nodes: [
    { id: "Python", group: 1, icon: "assets/img/python.png" },
    { id: "R", group: 1, icon: "assets/img/r.png" },
    { id: "SQL", group: 1, icon: "assets/img/sql.png" },
    { id: "Power BI", group: 2, icon: "assets/img/powerbi.png" },
    { id: "Azure", group: 3, icon: "assets/img/azure.png" },
    { id: "AWS", group: 3, icon: "assets/img/aws.png" },
    { id: "PySpark", group: 1, icon: "assets/img/pyspark.png" },
    { id: "D3.js", group: 4, icon: "assets/img/d3.png" },
    { id: "Bayesian Modeling", group: 5, icon: "assets/img/pymc3.png" },
    { id: "Machine Learning", group: 5, icon: "assets/img/ml.png" },
    { id: "IoT Analytics", group: 6, icon: "assets/img/iot.png" }
  ],
  links: [
    { source: "Python", target: "Power BI" },
    { source: "Python", target: "PySpark" },
    { source: "Python", target: "Machine Learning" },
    { source: "Machine Learning", target: "Bayesian Modeling" },
    { source: "Machine Learning", target: "IoT Analytics" },
    { source: "Azure", target: "IoT Analytics" },
    { source: "AWS", target: "IoT Analytics" },
    { source: "Power BI", target: "D3.js" },
    { source: "D3.js", target: "Python" },
    { source: "SQL", target: "Azure" }
  ]
};

const width2 = 700;
const height2 = 500;

const svgSkills = d3.select("#skills")
  .append("svg")
  .attr("width", "100%")
  .attr("height", height2)
  .style("background", "#0d1117")
  .style("border-radius", "10px");

const link = svgSkills.append("g")
  .selectAll("line")
  .data(skills.links)
  .enter().append("line")
  .attr("stroke", "#30363d")
  .attr("stroke-width", 1.5);

const node = svgSkills.selectAll(".node")
  .data(skills.nodes)
  .enter()
  .append("g")
  .attr("class", "node")
  .call(drag(simulation));

node.append("circle")
  .attr("r", 30)
  .attr("fill", "#21262d")
  .attr("stroke", "#58a6ff")
  .attr("stroke-width", 1.5);

node.append("image")
  .attr("xlink:href", d => d.icon)
  .attr("x", -20)
  .attr("y", -20)
  .attr("width", 40)
  .attr("height", 40)
  .attr("clip-path", "circle(20px at center)");

const simulation = d3.forceSimulation(skills.nodes)
  .force("link", d3.forceLink(skills.links).id(d => d.id).distance(140))
  .force("charge", d3.forceManyBody().strength(-400))
  .force("center", d3.forceCenter(width2 / 2, height2 / 2));

simulation.on("tick", () => {
  link
    .attr("x1", d => d.source.x)
    .attr("y1", d => d.source.y)
    .attr("x2", d => d.target.x)
    .attr("y2", d => d.target.y);

  node.attr("transform", d => `translate(${d.x}, ${d.y})`);
});

function drag(simulation) {
  function dragstarted(event) {
    if (!event.active) simulation.alphaTarget(0.3).restart();
    event.subject.fx = event.subject.x;
    event.subject.fy = event.subject.y;
  }
  function dragged(event) {
    event.subject.fx = event.x;
    event.subject.fy = event.y;
  }
  function dragended(event) {
    if (!event.active) simulation.alphaTarget(0);
    event.subject.fx = null;
    event.subject.fy = null;
  }
  return d3.drag().on("start", dragstarted).on("drag", dragged).on("end", dragended);
}
</script>
