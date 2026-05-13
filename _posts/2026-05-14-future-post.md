\---

layout: post

title: Future Post with spaces

author: Atthadassi

categories: 

tags: 

image: \[desktop.png]

\---



\# Title



this is a sentence



\## part 1



explanation of part 1



\### part 1.1

explanation of part 1.1



\## part 2

\### part 2.1

explanation of 2.1



List:

\- item 1

\- item 2

\- item 3

\- item 4







\---

<script>

document.addEventListener("DOMContentLoaded", function() {

&#x20; // Add styles for collapsible TOC

&#x20; const style = document.createElement("style");

&#x20; style.textContent = `

&#x20;   .table-of-contents {

&#x20;     background: #f5f5f0;

&#x20;     padding: 1rem 1.5rem;

&#x20;     border-radius: 8px;

&#x20;     margin-bottom: 2rem;

&#x20;     border-left: 4px solid #8B4513;

&#x20;   }

&#x20;   .table-of-contents h2 {

&#x20;     margin-top: 0;

&#x20;     font-size: 1.3rem;

&#x20;   }

&#x20;   .table-of-contents ul {

&#x20;     margin-bottom: 0;

&#x20;     padding-left: 1.2rem;

&#x20;   }

&#x20;   .table-of-contents li {

&#x20;     margin: 0.3rem 0;

&#x20;     list-style-type: none;

&#x20;   }

&#x20;   .table-of-contents a {

&#x20;     text-decoration: none;

&#x20;     color: #2c5e2e;

&#x20;   }

&#x20;   .table-of-contents a:hover {

&#x20;     text-decoration: underline;

&#x20;   }

&#x20;   /\* Collapsible section styles \*/

&#x20;   .toc-h2-item {

&#x20;     margin-top: 0.5rem;

&#x20;   }

&#x20;   .toc-h2-link {

&#x20;     cursor: pointer;

&#x20;     display: inline-block;

&#x20;   }

&#x20;   .toc-toggle {

&#x20;     cursor: pointer;

&#x20;     display: inline-block;

&#x20;     width: 20px;

&#x20;     font-size: 0.9rem;

&#x20;     font-weight: bold;

&#x20;     color: #8B4513;

&#x20;     user-select: none;

&#x20;     margin-right: 6px;

&#x20;     text-align: center;

&#x20;   }

&#x20;   .toc-toggle:hover {

&#x20;     color: #2c5e2e;

&#x20;   }

&#x20;   .toc-h3-list {

&#x20;     margin-left: 26px;

&#x20;     padding-left: 0;

&#x20;     transition: all 0.2s ease;

&#x20;   }

&#x20;   .toc-h3-list.collapsed {

&#x20;     display: none;

&#x20;   }

&#x20; `;

&#x20; document.head.appendChild(style);

&#x20; 

&#x20; // Generate TOC

&#x20; const headings = document.querySelectorAll("h2, h3");

&#x20; if (headings.length === 0) return;

&#x20; 

&#x20; const toc = document.createElement("div");

&#x20; toc.className = "table-of-contents";

&#x20; toc.innerHTML = "<h2>📖</h2><ul></ul>";

&#x20; const tocList = toc.querySelector("ul");

&#x20; 

&#x20; let currentH2Item = null;

&#x20; let currentH3List = null;

&#x20; 

&#x20; headings.forEach(heading => {

&#x20;   if (heading.closest(".table-of-contents")) return;

&#x20;   

&#x20;   if (!heading.id) {

&#x20;     heading.id = heading.textContent

&#x20;       .toLowerCase()

&#x20;       .replace(/\[🇧🇷🇪🇸🇬🇧]/g, "")

&#x20;       .replace(/\[^\\w\\s-]/g, "")

&#x20;       .replace(/\\s+/g, "-");

&#x20;   }

&#x20;   

&#x20;   if (heading.tagName === "H2") {

&#x20;     // Create container for this H2 section

&#x20;     const li = document.createElement("li");

&#x20;     li.className = "toc-h2-item";

&#x20;     

&#x20;     // Add toggle arrow

&#x20;     const toggle = document.createElement("span");

&#x20;     toggle.className = "toc-toggle";

&#x09;toggle.textContent = "▶";  // Collapsed by default

&#x20;     toggle.setAttribute("aria-label", "Collapse section");

&#x20;     

&#x20;     // Add the H2 link

&#x20;     const a = document.createElement("a");

&#x20;     a.href = `#${heading.id}`;

&#x20;     a.textContent = heading.textContent;

&#x20;     a.className = "toc-h2-link";

&#x20;     

&#x20;     // Container for H3 items (to be filled later)

&#x20;     const h3Container = document.createElement("ul");

&#x20;     h3Container.className = "toc-h3-list";

&#x20;     h3Container.classList.add("collapsed");

&#x09;  

&#x20;     // Assemble

&#x20;     li.appendChild(toggle);

&#x20;     li.appendChild(a);

&#x20;     li.appendChild(h3Container);

&#x20;     tocList.appendChild(li);

&#x20;     

&#x20;     // Store references

&#x20;     currentH2Item = li;

&#x20;     currentH3List = h3Container;

&#x20;     

&#x20;     // Add click toggle functionality

&#x20;     const toggleSection = () => {

&#x20;       const isCollapsed = h3Container.classList.contains("collapsed");

&#x20;       if (isCollapsed) {

&#x20;         h3Container.classList.remove("collapsed");

&#x20;         toggle.textContent = "▼";

&#x20;         toggle.setAttribute("aria-label", "Collapse section");

&#x20;       } else {

&#x20;         h3Container.classList.add("collapsed");

&#x20;         toggle.textContent = "▶";

&#x20;         toggle.setAttribute("aria-label", "Expand section");

&#x20;       }

&#x20;     };

&#x20;     

&#x20;     toggle.addEventListener("click", function(e) {

&#x20;       e.preventDefault();

&#x20;       e.stopPropagation();

&#x20;       toggleSection();

&#x20;     });

&#x20;     

&#x20;     a.addEventListener("click", function(e) {

&#x20;       // Allow normal anchor behavior, but also toggle if desired?

&#x20;       // Comment out the next line if you want clicking the link to ALSO toggle

&#x20;       // e.preventDefault(); 

&#x20;       // Uncomment below to toggle when clicking the link text too

&#x20;       // toggleSection();

&#x20;       // Then scroll to heading

&#x20;       // document.getElementById(heading.id).scrollIntoView({ behavior: "smooth" });

&#x20;     });

&#x20;     

&#x20;   } else if (heading.tagName === "H3" \&\& currentH3List) {

&#x20;     // Add H3 item under current H2

&#x20;     const li = document.createElement("li");

&#x20;     const a = document.createElement("a");

&#x20;     a.href = `#${heading.id}`;

&#x20;     a.textContent = heading.textContent;

&#x20;     li.appendChild(a);

&#x20;     currentH3List.appendChild(li);

&#x20;   }

&#x20; });

&#x20; 

&#x20; // Insert TOC at the beginning of the page

&#x20; const firstHeading = document.querySelector("h1, h2");

&#x20; if (firstHeading) {

&#x20;   firstHeading.parentNode.insertBefore(toc, firstHeading);

&#x20; } else {

&#x20;   document.body.insertBefore(toc, document.body.firstChild);

&#x20; }

});

</script>

&#x09;





