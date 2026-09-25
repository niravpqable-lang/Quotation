<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="theme-color" content="#111827" />
  <title>Harikrishna Tubewell - Quotation Builder</title>
  <script src="https://cdn.jsdelivr.net/npm/html2pdf.js@0.10.1/dist/html2pdf.bundle.min.js"></script>
  <style>
    :root{
      --bg:#eef5ff;--card:#ffffff;--ink:#172033;--muted:#64748b;--line:#cbd5e1;
      --accent:#2563eb;--accent2:#0f766e;--soft:#eff6ff;--danger:#dc2626;--gold:#f59e0b;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Arial,Helvetica,sans-serif;background:var(--bg);color:var(--ink)}
    button,input,select,textarea{font:inherit}
    .topbar{position:sticky;top:0;z-index:20;background:linear-gradient(135deg,#0f172a,#1d4ed8);border-bottom:1px solid #1e40af;padding:12px 18px;display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap;box-shadow:0 6px 18px rgba(15,23,42,.18)}
    .brand{font-weight:900;font-size:20px;color:#fff;letter-spacing:.2px}.brand small{display:block;color:#bfdbfe;font-weight:600;font-size:12px;margin-top:2px}
    .actions{display:flex;gap:8px;flex-wrap:wrap}
    .btn{border:1px solid #cbd5e1;background:#fff;color:#172033;padding:9px 13px;border-radius:9px;cursor:pointer;font-weight:800;box-shadow:0 1px 2px rgba(15,23,42,.06);transition:.18s ease}
    .btn:hover{background:#eff6ff;border-color:#93c5fd;transform:translateY(-1px)}
    .btn.primary{background:linear-gradient(135deg,#16a34a,#059669);color:#fff;border-color:#059669;box-shadow:0 5px 14px rgba(5,150,105,.25)}
    .btn.danger{color:var(--danger)}
    .shell{max-width:1500px;margin:0 auto;padding:18px;display:grid;grid-template-columns:minmax(360px,1fr) minmax(500px,1.1fr);gap:18px;align-items:start}
    .panel{background:#fff;border:1px solid #dbeafe;border-radius:16px;box-shadow:0 10px 30px rgba(37,99,235,.09);overflow:hidden}
    .panel-head{padding:18px;border-bottom:1px solid #dbeafe;background:linear-gradient(180deg,#ffffff,#f8fbff)}
    .panel-head h1,.panel-head h2{margin:0;color:#1e3a8a}.panel-head p{margin:6px 0 0;color:var(--muted)}
    .section{padding:18px;border-top:1px solid #e6eef8}.section:first-child{border-top:0}
    .section-title{display:flex;gap:10px;align-items:flex-start;margin-bottom:14px}.step{width:36px;height:36px;border-radius:10px;background:linear-gradient(135deg,#2563eb,#0ea5e9);color:#fff;display:grid;place-items:center;font-size:12px;font-weight:900;box-shadow:0 5px 12px rgba(37,99,235,.22)}
    .section-title h3{margin:0;font-size:16px}.section-title p{margin:3px 0 0;font-size:12px;color:var(--muted)}
    .grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px}.grid3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px}
    .field label{display:block;font-size:12px;font-weight:700;margin-bottom:5px}.field input,.field select,.field textarea{width:100%;border:1px solid #cbd5e1;border-radius:9px;padding:10px 11px;background:#fff;outline:none;transition:.15s ease}
    .field input:focus,.field select:focus,.field textarea:focus{border-color:#3b82f6;box-shadow:0 0 0 3px rgba(59,130,246,.12)}
    .field textarea{min-height:64px;resize:vertical}
    .preset-row{display:flex;gap:8px;align-items:end;flex-wrap:wrap}.preset-row .field{flex:1;min-width:220px}
    .items{display:flex;flex-direction:column;gap:10px}
    .item-card{border:1px solid #dbeafe;border-radius:12px;padding:12px;background:linear-gradient(180deg,#ffffff,#f8fbff);box-shadow:0 3px 10px rgba(37,99,235,.05)}
    .item-top{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-bottom:9px}.item-title{font-size:13px;font-weight:800}
    .remove{border:0;background:transparent;color:#b91c1c;font-weight:800;cursor:pointer;padding:4px 6px}
    .item-grid{display:grid;grid-template-columns:minmax(210px,2fr) 88px 105px 110px 130px;gap:8px;align-items:end}
    .calc{padding:10px 10px;border:1px solid #bfdbfe;border-radius:8px;background:#eff6ff;color:#1d4ed8;white-space:nowrap;text-align:right;font-weight:900}
    .grand{margin-top:14px;display:flex;justify-content:space-between;align-items:center;border:1px solid #bbf7d0;background:linear-gradient(135deg,#f0fdf4,#dcfce7);padding:13px 15px;border-radius:10px;font-weight:900;font-size:19px;color:#166534}
    .notes{display:flex;flex-direction:column;gap:8px}.note-row{display:grid;grid-template-columns:1fr auto;gap:8px}
    .note-row input{width:100%;border:1px solid #cbd5e1;border-radius:7px;padding:9px 10px}
    .preview-wrap{padding:18px;overflow:auto}.preview-label{display:flex;justify-content:space-between;color:#1d4ed8;font-size:12px;font-weight:800;margin-bottom:10px;background:#eff6ff;border:1px solid #dbeafe;padding:8px 10px;border-radius:8px}
    #pdfArea{width:210mm;min-height:297mm;background:#fff;margin:auto;padding:14mm 12mm 12mm;color:#000;box-shadow:0 8px 28px rgba(15,23,42,.16);border-top:5px solid #2563eb}
    .pdf-header{text-align:center}.pdf-header h1{font-size:24px;margin:0 0 5px;font-weight:900;color:#1e3a8a}.pdf-header .addr{font-size:11px;line-height:1.35;color:#334155}
    .pdf-title{margin-top:12px;text-align:center;font-size:18px;font-weight:900;color:#0f766e;text-decoration:underline}
    .pdf-meta{margin-top:10px;font-size:12px;display:grid;grid-template-columns:1fr auto;gap:8px}.pdf-meta div{min-height:17px}
    .pdf-subject{text-align:center;font-size:13px;font-weight:800;margin:10px 0 8px;text-decoration:underline}
    table{width:100%;border-collapse:collapse;font-size:10.5px}th,td{border:1px solid #334155;padding:5px 5px;vertical-align:top}th{text-align:center;font-weight:900;background:#dbeafe;color:#1e3a8a}
    td.num{text-align:right;white-space:nowrap}td.center{text-align:center}.no{width:34px}.unit{width:74px}.rate{width:75px}.amt{width:90px}
    .total-row td{font-weight:900;font-size:11.5px;border-top:2px solid #166534;background:#f0fdf4;color:#166534}
    .pdf-notes{font-size:10.5px;margin-top:9px;line-height:1.45}.pdf-notes .note{display:flex;gap:5px}
    .pdf-contact{font-size:11px;font-weight:800;margin-top:14px}
    .footer-note{font-size:9px;color:#555;margin-top:8px;text-align:center}
    .status{font-size:12px;color:#d1fae5;font-weight:800;background:rgba(16,185,129,.16);padding:5px 8px;border-radius:999px}.hide{display:none}
    @media (max-width:1050px){.shell{grid-template-columns:1fr}.item-grid{grid-template-columns:1fr 90px 110px}.item-grid .field:nth-child(4),.item-grid .calc{grid-column:auto}.preview-wrap{padding:10px}#pdfArea{transform-origin:top left}}
    @media (max-width:650px){.shell{padding:8px}.grid2,.grid3{grid-template-columns:1fr}.item-grid{grid-template-columns:1fr 1fr}.item-grid .field:first-child{grid-column:1/-1}.calc{grid-column:1/-1}.topbar{padding:10px}.panel{border-radius:8px}}
    @media print{
      body{background:#fff}.topbar,.editor-panel,.preview-label{display:none!important}.shell{display:block;padding:0;max-width:none}.preview-panel{border:0;box-shadow:none}.preview-wrap{padding:0;overflow:visible}
      #pdfArea{box-shadow:none;margin:0;width:210mm;min-height:297mm;padding:14mm 12mm 12mm}
      @page{size:A4 portrait;margin:0}
    }
  </style>
</head>
<body>
  <div class="topbar">
    <div class="brand">H Quotation Builder<small>Harikrishna Tubewell • Professional Quotation System</small></div>
    <div class="actions">
      <span id="status" class="status"></span>
      <button class="btn" onclick="startNew()">Start new</button>
      <button class="btn" onclick="saveDraft()">Save draft</button>
      <button class="btn" onclick="window.print()">Print / Save PDF</button>
      <button class="btn primary" onclick="downloadPDF()">Download PDF</button>
    </div>
  </div>

  <main class="shell">
    <section class="panel editor-panel">
      <div class="panel-head">
        <h1>Quotation Editor</h1>
        <p>Create a quotation. Changes appear instantly in the preview.</p>
      </div>

      <div class="section">
        <div class="section-title"><div class="step">01</div><div><h3>Business & customer</h3><p>The business heading stays on the PDF and can be changed here.</p></div></div>
        <div class="grid2">
          <div class="field"><label>Business heading</label><input id="business" value="Harikrishna Tubewell Co."></div>
          <div class="field"><label>Business address</label><input id="address" value="B-37 CP Nagar Society Part-2, Bhuyangdev, Ghatlodiya, Ahmedabad, Gujarat-380061"></div>
          <div class="field"><label>To / customer</label><input id="customer" placeholder="Customer name"></div>
          <div class="field"><label>Site</label><input id="site" placeholder="Site"></div>
          <div class="field"><label>Date</label><input id="qdate" type="date"></div>
          <div class="field"><label>Quotation title</label><input id="title" value='6" DIA MS TUBEWELL - 700 ft'></div>
          <div class="field" style="grid-column:1/-1"><label>Contact person</label><input id="contact" value="Suresh Patel - +91 9825455897"></div>
        </div>
      </div>

      <div class="section">
        <div class="section-title"><div class="step">02</div><div><h3>Items & rates</h3><p>Choose a reference list or add your own lines. Leave rate empty to enter a fixed amount.</p></div></div>
        <div class="preset-row">
          <div class="field"><label>Start with</label>
            <select id="preset">
              <option value="xavier">MS tubewell · Xt. Xavier</option>
              <option value="satellite">MS tubewell · Satellite</option>
              <option value="cement">Cement fiber · Rashmi</option>
              <option value="blank">Blank quotation</option>
            </select>
          </div>
          <button class="btn" onclick="loadPreset()">Load items</button>
        </div>
        <div id="items" class="items" style="margin-top:12px"></div>
        <button class="btn" style="margin-top:10px" onclick="addItem()">+ Add custom item</button>
        <div class="grand"><span>Grand Total</span><span id="grandTotal">₹0</span></div>
      </div>

      <div class="section">
        <div class="section-title"><div class="step">03</div><div><h3>Notes</h3><p>Reference notes are included automatically. Edit or remove any line.</p></div></div>
        <div id="notes" class="notes"></div>
        <button class="btn" style="margin-top:10px" onclick="addNote()">+ Add note</button>
      </div>
    </section>

    <section class="panel preview-panel">
      <div class="panel-head">
        <h2>Live Preview</h2>
        <p>PDF layout · A4 portrait</p>
      </div>
      <div class="preview-wrap">
        <div class="preview-label"><span>Quotation preview</span><span>Ready to download</span></div>
        <div id="pdfArea">
          <div class="pdf-header">
            <h1 id="pBusiness"></h1>
            <div class="addr" id="pAddress"></div>
          </div>
          <div class="pdf-title">Quotation</div>
          <div class="pdf-meta">
            <div><b>To :-</b> <span id="pCustomer"></span></div>
            <div><b>Date :-</b> <span id="pDate"></span></div>
            <div><b>Site :-</b> <span id="pSite"></span></div>
            <div></div>
          </div>
          <div class="pdf-subject" id="pTitle"></div>
          <table>
            <thead><tr><th class="no">NO.</th><th>PARTICULARS</th><th class="unit">UNIT</th><th class="rate">RATE</th><th class="amt">AMOUNT</th></tr></thead>
            <tbody id="pRows"></tbody>
            <tfoot><tr class="total-row"><td colspan="4" style="text-align:right">Grand Total</td><td class="num" id="pTotal"></td></tr></tfoot>
          </table>
          <div class="pdf-notes"><b>Note:-</b><div id="pNotes"></div></div>
          <div class="pdf-contact">Contact person:- <span id="pContact"></span></div>
        </div>
      </div>
    </section>
  </main>

<script>
const units = ["ft","Job","Gaadi","Meter","mt","Set","Approx","Tons","Nos","Piece","Litre","Day","Other"];

const xavierItems = [
  {p:'6" 5mm (4.70mm) MS pipe Heavy Jindal Brand',q:700,u:'ft',r:510,a:''},
  {p:'Pipe Accessories / Stenar chapla heavy / facing / loading / unloading / transportation charge',q:1,u:'Job',r:'',a:55000},
  {p:'Drilling labour charge',q:710,u:'ft',r:330,a:''},
  {p:'Gravel special 8-10mm',q:17,u:'Tons',r:2200,a:''},
  {p:'Clay ball (407 metador)',q:1,u:'Gaadi',r:'',a:8500},
  {p:'Gravel packing and clay packing labour charge',q:1,u:'Job',r:'',a:13000},
  {p:'Airline with compressor (Heavy 1200/300)',q:1,u:'Job',r:'',a:35000},
  {p:'6hp 31-stage V4 Varuna brand submersible pump set',q:1,u:'Set',r:'',a:43500},
  {p:'Ashirvad brand UPVC column pipe 1.5" Standard',q:47,u:'Nos',r:850,a:''},
  {p:'Column pipe accessories and transportation charge',q:1,u:'Job',r:'',a:4500},
  {p:'Dharshan brand ISI 2.5mm flat cable',q:160,u:'mt',r:135,a:''},
  {p:'C&S brand Dior panel board',q:1,u:'Set',r:'',a:11000},
  {p:'Motor loading charge in bore',q:1,u:'Job',r:'',a:3000},
  {p:'17×17×7 Mudpit Chokdi JCB work',q:1,u:'Job',r:'',a:6000},
  {p:'Water Tanker',q:45,u:'Approx',r:700,a:''},
  {p:'Mud Tanker',q:30,u:'Approx',r:1500,a:''}
];

const defaultNotes = [
  'No. 1, 8, 9, 10, 11, 12 including GST rate.',
  'No. 2, 3, 4, 5, 6, 7, 13 labour bill.',
  'No. 1, 8, 9, 10, 11, 12 rate will be considered on the day of purchase.'
];

let items = JSON.parse(JSON.stringify(xavierItems));
let notes = [...defaultNotes];

function money(n){
  const v = Number(n||0);
  return '₹' + v.toLocaleString('en-IN', {maximumFractionDigits:2});
}
function amount(i){
  const q = Number(i.q||0), r = Number(i.r||0), a = Number(i.a||0);
  return i.r !== '' && i.r !== null && String(i.r).trim() !== '' ? q*r : a;
}
function esc(s){
  return String(s??'').replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]));
}
function unitOptions(sel){
  return units.map(u=>`<option ${u===sel?'selected':''}>${u}</option>`).join('');
}
function renderItems(){
  const box=document.getElementById('items'); box.innerHTML='';
  items.forEach((i,idx)=>{
    const div=document.createElement('div'); div.className='item-card';
    div.innerHTML=`
      <div class="item-top"><div class="item-title">Item ${idx+1}</div><button class="remove" onclick="removeItem(${idx})">Remove ×</button></div>
      <div class="item-grid">
        <div class="field"><label>Particulars</label><textarea oninput="setItem(${idx},'p',this.value)">${esc(i.p)}</textarea></div>
        <div class="field"><label>Quantity</label><input type="number" step="any" value="${esc(i.q)}" oninput="setItem(${idx},'q',this.value)"></div>
        <div class="field"><label>Unit</label><select onchange="setItem(${idx},'u',this.value)">${unitOptions(i.u)}</select></div>
        <div class="field"><label>Rate ₹</label><input type="number" step="any" value="${esc(i.r)}" placeholder="Optional" oninput="setItem(${idx},'r',this.value)"></div>
        <div>
          ${String(i.r).trim()===''?`<div class="field"><label>Fixed amount ₹</label><input type="number" step="any" value="${esc(i.a)}" oninput="setItem(${idx},'a',this.value)"></div>`:`<label style="display:block;font-size:12px;font-weight:700;margin-bottom:5px">Amount</label><div class="calc">${money(amount(i))}</div>`}
        </div>
      </div>`;
    box.appendChild(div);
  });
  updatePreview();
}
function setItem(idx,key,val){
  items[idx][key]=val;
  if(key==='r') renderItems(); else updatePreview();
}
function addItem(){items.push({p:'',q:1,u:'Job',r:'',a:''});renderItems()}
function removeItem(idx){items.splice(idx,1);renderItems()}
function renderNotes(){
  const box=document.getElementById('notes');box.innerHTML='';
  notes.forEach((n,idx)=>{
    const row=document.createElement('div');row.className='note-row';
    row.innerHTML=`<input value="${esc(n)}" oninput="notes[${idx}]=this.value;updatePreview()"><button class="remove" onclick="notes.splice(${idx},1);renderNotes();updatePreview()">Remove ×</button>`;
    box.appendChild(row);
  }); updatePreview();
}
function addNote(){notes.push('');renderNotes()}

function formattedDate(v){
  if(!v) return '';
  const d=new Date(v+'T00:00:00');
  return d.toLocaleDateString('en-GB',{day:'2-digit',month:'long',year:'numeric'});
}
function updatePreview(){
  document.getElementById('pBusiness').textContent=document.getElementById('business').value;
  document.getElementById('pAddress').textContent=document.getElementById('address').value;
  document.getElementById('pCustomer').textContent=document.getElementById('customer').value;
  document.getElementById('pSite').textContent=document.getElementById('site').value;
  document.getElementById('pDate').textContent=formattedDate(document.getElementById('qdate').value);
  document.getElementById('pTitle').textContent=document.getElementById('title').value;
  document.getElementById('pContact').textContent=document.getElementById('contact').value;

  const rows=document.getElementById('pRows'); rows.innerHTML='';
  let total=0;
  items.forEach((i,idx)=>{
    const a=amount(i); total+=a;
    const tr=document.createElement('tr');
    tr.innerHTML=`<td class="center">${idx+1}</td><td>${esc(i.p)}</td><td class="center">${esc(i.q)} ${esc(i.u)}</td><td class="num">${String(i.r).trim()!==''?Number(i.r).toLocaleString('en-IN'):''}</td><td class="num">${a?Number(a).toLocaleString('en-IN'):''}</td>`;
    rows.appendChild(tr);
  });
  document.getElementById('pTotal').textContent=Number(total).toLocaleString('en-IN');
  document.getElementById('grandTotal').textContent=money(total);

  const pn=document.getElementById('pNotes');pn.innerHTML='';
  notes.filter(n=>n.trim()).forEach((n,idx)=>{
    const d=document.createElement('div');d.className='note';
    d.innerHTML=`<span>(${String.fromCharCode(65+idx)})</span><span>${esc(n)}</span>`;
    pn.appendChild(d);
  });
}

function loadPreset(){
  const p=document.getElementById('preset').value;
  if(p==='blank') items=[{p:'',q:1,u:'Job',r:'',a:''}];
  else items=JSON.parse(JSON.stringify(xavierItems));
  if(p==='satellite') document.getElementById('title').value='6" DIA MS TUBEWELL';
  if(p==='cement') {
    items=[
      {p:'Cement fiber pipe',q:1,u:'ft',r:'',a:''},
      {p:'Drilling labour charge',q:1,u:'ft',r:'',a:''},
      {p:'Transportation / loading / unloading',q:1,u:'Job',r:'',a:''}
    ];
    document.getElementById('title').value='CEMENT FIBER TUBEWELL';
  }
  renderItems();
}

function collectDraft(){
  return {
    business:business.value,address:address.value,customer:customer.value,site:site.value,qdate:qdate.value,
    title:title.value,contact:contact.value,items,notes
  };
}
function saveDraft(){
  localStorage.setItem('harikrishnaQuotationDraft',JSON.stringify(collectDraft()));
  flash('Draft saved on this device');
}
function loadDraft(){
  try{
    const d=JSON.parse(localStorage.getItem('harikrishnaQuotationDraft')||'null');
    if(!d) return false;
    business.value=d.business||'';address.value=d.address||'';customer.value=d.customer||'';site.value=d.site||'';
    qdate.value=d.qdate||'';title.value=d.title||'';contact.value=d.contact||'';items=d.items||[];notes=d.notes||[];
    return true;
  }catch(e){return false}
}
function startNew(){
  if(!confirm('Start a new quotation? Current unsaved changes will be cleared.')) return;
  customer.value='';site.value='';title.value='6" DIA MS TUBEWELL - 700 ft';qdate.value=new Date().toISOString().slice(0,10);
  items=JSON.parse(JSON.stringify(xavierItems));notes=[...defaultNotes];renderItems();renderNotes();
}
function flash(msg){
  const el=document.getElementById('status'); el.textContent=msg; setTimeout(()=>el.textContent='',2500);
}
async function downloadPDF(){
  updatePreview();
  const el=document.getElementById('pdfArea');
  const customerName=(document.getElementById('customer').value||'Quotation').replace(/[^a-z0-9_-]+/gi,'_');
  const filename=`Harikrishna_Quotation_${customerName}.pdf`;

  if(typeof html2pdf === 'undefined'){
    alert('PDF library could not load. Please use "Print / Save PDF" instead.');
    window.print();
    return;
  }
  flash('Preparing PDF…');
  const opt={
    margin:0,
    filename,
    image:{type:'jpeg',quality:0.98},
    html2canvas:{scale:2,useCORS:true,letterRendering:true,scrollY:0},
    jsPDF:{unit:'mm',format:'a4',orientation:'portrait'},
    pagebreak:{mode:['css','legacy'],avoid:['tr','.pdf-contact']}
  };
  try{
    await html2pdf().set(opt).from(el).save();
    flash('PDF downloaded');
  }catch(e){
    alert('Direct download could not start. Use "Print / Save PDF" as a backup.');
  }
}

['business','address','customer','site','qdate','title','contact'].forEach(id=>{
  document.getElementById(id).addEventListener('input',updatePreview);
});
if(!loadDraft()) document.getElementById('qdate').value=new Date().toISOString().slice(0,10);
renderItems();renderNotes();updatePreview();
</script>
</body>
</html>
