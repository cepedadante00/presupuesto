import { useState, useEffect, useCallback } from "react";
import { PieChart, Pie, Cell, BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";

const CATEGORIES = {
  income: ["Salario", "Freelance", "Inversiones", "Regalo", "Otro ingreso"],
  expense: ["Comida", "Transporte", "Hogar", "Salud", "Entretenimiento", "Ropa", "Educación", "Otro gasto"],
};

const CAT_COLORS = {
  "Salario": "#4ade80", "Freelance": "#34d399", "Inversiones": "#2dd4bf", "Regalo": "#a3e635", "Otro ingreso": "#86efac",
  "Comida": "#f87171", "Transporte": "#fb923c", "Hogar": "#fbbf24", "Salud": "#e879f9", "Entretenimiento": "#60a5fa",
  "Ropa": "#f472b6", "Educación": "#818cf8", "Otro gasto": "#94a3b8",
};

const MONTHS = ["Ene","Feb","Mar","Abr","May","Jun","Jul","Ago","Sep","Oct","Nov","Dic"];

function formatCurrency(n) {
  return new Intl.NumberFormat("es-MX", { style: "currency", currency: "MXN", maximumFractionDigits: 0 }).format(n);
}

const STORAGE_KEY = "budget-app-data-v1";

async function loadData() {
  try {
    const result = await window.storage.get(STORAGE_KEY);
    return result ? JSON.parse(result.value) : [];
  } catch {
    return [];
  }
}

async function saveData(transactions) {
  try {
    await window.storage.set(STORAGE_KEY, JSON.stringify(transactions));
  } catch (e) {
    console.error("Error saving:", e);
  }
}

export default function BudgetApp() {
  const [tab, setTab] = useState("home");
  const [transactions, setTransactions] = useState([]);
  const [loading, setLoading] = useState(true);
  const [showForm, setShowForm] = useState(false);
  const [form, setForm] = useState({ type: "expense", amount: "", category: "Comida", note: "", date: new Date().toISOString().slice(0, 10) });
  const [filterMonth, setFilterMonth] = useState(new Date().getMonth());
  const [filterYear, setFilterYear] = useState(new Date().getFullYear());

  useEffect(() => {
    loadData().then(d => { setTransactions(d); setLoading(false); });
  }, []);

  const addTransaction = useCallback(async () => {
    if (!form.amount || isNaN(parseFloat(form.amount))) return;
    const tx = { id: Date.now(), ...form, amount: parseFloat(form.amount) };
    const updated = [tx, ...transactions];
    setTransactions(updated);
    await saveData(updated);
    setShowForm(false);
    setForm({ type: "expense", amount: "", category: "Comida", note: "", date: new Date().toISOString().slice(0, 10) });
    setTab("home");
  }, [form, transactions]);

  const deleteTransaction = useCallback(async (id) => {
    const updated = transactions.filter(t => t.id !== id);
    setTransactions(updated);
    await saveData(updated);
  }, [transactions]);

  const filtered = transactions.filter(t => {
    const d = new Date(t.date + "T12:00:00");
    return d.getMonth() === filterMonth && d.getFullYear() === filterYear;
  });

  const income = filtered.filter(t => t.type === "income").reduce((s, t) => s + t.amount, 0);
  const expense = filtered.filter(t => t.type === "expense").reduce((s, t) => s + t.amount, 0);
  const balance = income - expense;

  // Chart data
  const expenseByCat = CATEGORIES.expense.map(cat => ({
    name: cat, value: filtered.filter(t => t.type === "expense" && t.category === cat).reduce((s, t) => s + t.amount, 0)
  })).filter(d => d.value > 0);

  const last6 = Array.from({ length: 6 }, (_, i) => {
    const d = new Date(filterYear, filterMonth - 5 + i, 1);
    const m = d.getMonth(); const y = d.getFullYear();
    const txs = transactions.filter(t => { const td = new Date(t.date + "T12:00:00"); return td.getMonth() === m && td.getFullYear() === y; });
    return {
      name: MONTHS[m],
      Ingresos: txs.filter(t => t.type === "income").reduce((s, t) => s + t.amount, 0),
      Gastos: txs.filter(t => t.type === "expense").reduce((s, t) => s + t.amount, 0),
    };
  });

  const changeMonth = (dir) => {
    let m = filterMonth + dir, y = filterYear;
    if (m < 0) { m = 11; y--; }
    if (m > 11) { m = 0; y++; }
    setFilterMonth(m); setFilterYear(y);
  };

  if (loading) return (
    <div style={{ minHeight: "100svh", background: "#0a0a0f", display: "flex", alignItems: "center", justifyContent: "center" }}>
      <div style={{ color: "#7c6af7", fontSize: 28 }}>●</div>
    </div>
  );

  return (
    <div style={{ minHeight: "100svh", background: "#0a0a0f", color: "#f1f0ff", fontFamily: "'DM Sans', sans-serif", maxWidth: 430, margin: "0 auto", display: "flex", flexDirection: "column", position: "relative" }}>
      <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600;700&family=Space+Grotesk:wght@600;700&display=swap" rel="stylesheet" />

      {/* HEADER */}
      <div style={{ padding: "52px 24px 20px", background: "linear-gradient(180deg, #13101e 0%, #0a0a0f 100%)" }}>
        <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between" }}>
          <div>
            <p style={{ margin: 0, fontSize: 12, color: "#6b6880", letterSpacing: 2, textTransform: "uppercase" }}>Mi Presupuesto</p>
            <div style={{ display: "flex", alignItems: "center", gap: 12, marginTop: 4 }}>
              <button onClick={() => changeMonth(-1)} style={{ background: "none", border: "none", color: "#7c6af7", fontSize: 18, cursor: "pointer", padding: 0 }}>‹</button>
              <h1 style={{ margin: 0, fontSize: 22, fontFamily: "'Space Grotesk', sans-serif", fontWeight: 700, color: "#f1f0ff" }}>
                {MONTHS[filterMonth]} {filterYear}
              </h1>
              <button onClick={() => changeMonth(1)} style={{ background: "none", border: "none", color: "#7c6af7", fontSize: 18, cursor: "pointer", padding: 0 }}>›</button>
            </div>
          </div>
          <button onClick={() => { setShowForm(true); setTab("add"); }}
            style={{ width: 44, height: 44, borderRadius: 14, background: "linear-gradient(135deg,#7c6af7,#9f8fff)", border: "none", color: "#fff", fontSize: 24, cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center", boxShadow: "0 4px 20px #7c6af740" }}>
            +
          </button>
        </div>
      </div>

      {/* BALANCE CARD */}
      <div style={{ margin: "0 20px 20px", padding: "24px", background: "linear-gradient(135deg,#1a1630,#12102a)", borderRadius: 24, border: "1px solid #2a2545", boxShadow: "0 8px 40px #00000060" }}>
        <p style={{ margin: "0 0 4px", fontSize: 12, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Balance</p>
        <p style={{ margin: "0 0 20px", fontSize: 36, fontFamily: "'Space Grotesk',sans-serif", fontWeight: 700, color: balance >= 0 ? "#7fffb8" : "#ff7070", letterSpacing: -1 }}>
          {formatCurrency(balance)}
        </p>
        <div style={{ display: "flex", gap: 12 }}>
          <div style={{ flex: 1, background: "#ffffff08", borderRadius: 14, padding: "12px 14px" }}>
            <p style={{ margin: "0 0 2px", fontSize: 11, color: "#4ade80", letterSpacing: 1, textTransform: "uppercase" }}>↑ Ingresos</p>
            <p style={{ margin: 0, fontSize: 16, fontWeight: 600, color: "#f1f0ff" }}>{formatCurrency(income)}</p>
          </div>
          <div style={{ flex: 1, background: "#ffffff08", borderRadius: 14, padding: "12px 14px" }}>
            <p style={{ margin: "0 0 2px", fontSize: 11, color: "#f87171", letterSpacing: 1, textTransform: "uppercase" }}>↓ Gastos</p>
            <p style={{ margin: 0, fontSize: 16, fontWeight: 600, color: "#f1f0ff" }}>{formatCurrency(expense)}</p>
          </div>
        </div>
      </div>

      {/* TABS */}
      <div style={{ display: "flex", margin: "0 20px 20px", background: "#13101e", borderRadius: 14, padding: 4, gap: 4 }}>
        {["home", "charts", "list"].map(t => (
          <button key={t} onClick={() => setTab(t)}
            style={{ flex: 1, padding: "10px 0", borderRadius: 10, border: "none", cursor: "pointer", fontSize: 12, fontWeight: 600, transition: "all .2s",
              background: tab === t ? "linear-gradient(135deg,#7c6af7,#9f8fff)" : "transparent",
              color: tab === t ? "#fff" : "#6b6880", boxShadow: tab === t ? "0 2px 12px #7c6af740" : "none" }}>
            {t === "home" ? "🏠 Inicio" : t === "charts" ? "📊 Gráficas" : "📋 Lista"}
          </button>
        ))}
      </div>

      {/* CONTENT */}
      <div style={{ flex: 1, padding: "0 20px", paddingBottom: 30 }}>

        {/* HOME TAB */}
        {tab === "home" && (
          <div>
            <p style={{ margin: "0 0 12px", fontSize: 13, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Últimos movimientos</p>
            {filtered.length === 0 && (
              <div style={{ textAlign: "center", padding: "40px 0", color: "#3d3858" }}>
                <div style={{ fontSize: 40, marginBottom: 8 }}>💸</div>
                <p style={{ margin: 0, fontSize: 14 }}>Sin movimientos este mes</p>
                <p style={{ margin: "4px 0 0", fontSize: 12 }}>Toca + para agregar uno</p>
              </div>
            )}
            {filtered.slice(0, 15).map(t => (
              <div key={t.id} style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "14px 16px", background: "#13101e", borderRadius: 16, marginBottom: 8, border: "1px solid #1e1a30" }}>
                <div style={{ display: "flex", alignItems: "center", gap: 12 }}>
                  <div style={{ width: 38, height: 38, borderRadius: 12, background: t.type === "income" ? "#4ade8020" : "#f8717120", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 16 }}>
                    {t.type === "income" ? "↑" : "↓"}
                  </div>
                  <div>
                    <p style={{ margin: 0, fontSize: 14, fontWeight: 600, color: "#f1f0ff" }}>{t.category}</p>
                    <p style={{ margin: 0, fontSize: 11, color: "#6b6880" }}>{t.note || t.date}</p>
                  </div>
                </div>
                <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                  <p style={{ margin: 0, fontSize: 15, fontWeight: 700, color: t.type === "income" ? "#4ade80" : "#f87171" }}>
                    {t.type === "income" ? "+" : "-"}{formatCurrency(t.amount)}
                  </p>
                  <button onClick={() => deleteTransaction(t.id)} style={{ background: "none", border: "none", color: "#3d3858", cursor: "pointer", fontSize: 16, padding: 0, lineHeight: 1 }}>×</button>
                </div>
              </div>
            ))}
          </div>
        )}

        {/* CHARTS TAB */}
        {tab === "charts" && (
          <div>
            <p style={{ margin: "0 0 16px", fontSize: 13, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Gastos por categoría</p>
            {expenseByCat.length === 0 ? (
              <div style={{ textAlign: "center", padding: "30px 0", color: "#3d3858" }}>
                <div style={{ fontSize: 36, marginBottom: 8 }}>📊</div>
                <p style={{ margin: 0, fontSize: 14 }}>Sin gastos este mes</p>
              </div>
            ) : (
              <>
                <div style={{ background: "#13101e", borderRadius: 20, padding: "20px 0", border: "1px solid #1e1a30", marginBottom: 16 }}>
                  <ResponsiveContainer width="100%" height={200}>
                    <PieChart>
                      <Pie data={expenseByCat} cx="50%" cy="50%" innerRadius={55} outerRadius={85} paddingAngle={3} dataKey="value">
                        {expenseByCat.map((e, i) => <Cell key={i} fill={CAT_COLORS[e.name] || "#7c6af7"} />)}
                      </Pie>
                      <Tooltip formatter={v => formatCurrency(v)} contentStyle={{ background: "#1a1630", border: "1px solid #2a2545", borderRadius: 10, color: "#f1f0ff" }} />
                    </PieChart>
                  </ResponsiveContainer>
                </div>
                <div style={{ display: "flex", flexWrap: "wrap", gap: 8, marginBottom: 20 }}>
                  {expenseByCat.map((e, i) => (
                    <div key={i} style={{ display: "flex", alignItems: "center", gap: 6, background: "#13101e", borderRadius: 20, padding: "6px 12px", border: "1px solid #1e1a30" }}>
                      <div style={{ width: 8, height: 8, borderRadius: "50%", background: CAT_COLORS[e.name] || "#7c6af7" }} />
                      <span style={{ fontSize: 11, color: "#c4c0d8" }}>{e.name}</span>
                      <span style={{ fontSize: 11, fontWeight: 700, color: "#f1f0ff" }}>{formatCurrency(e.value)}</span>
                    </div>
                  ))}
                </div>
              </>
            )}

            <p style={{ margin: "0 0 16px", fontSize: 13, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Últimos 6 meses</p>
            <div style={{ background: "#13101e", borderRadius: 20, padding: "20px 8px", border: "1px solid #1e1a30" }}>
              <ResponsiveContainer width="100%" height={180}>
                <BarChart data={last6} barGap={4}>
                  <XAxis dataKey="name" tick={{ fill: "#6b6880", fontSize: 11 }} axisLine={false} tickLine={false} />
                  <YAxis hide />
                  <Tooltip formatter={v => formatCurrency(v)} contentStyle={{ background: "#1a1630", border: "1px solid #2a2545", borderRadius: 10, color: "#f1f0ff" }} />
                  <Bar dataKey="Ingresos" fill="#4ade80" radius={[6, 6, 0, 0]} />
                  <Bar dataKey="Gastos" fill="#f87171" radius={[6, 6, 0, 0]} />
                </BarChart>
              </ResponsiveContainer>
            </div>
          </div>
        )}

        {/* LIST TAB */}
        {tab === "list" && (
          <div>
            <p style={{ margin: "0 0 12px", fontSize: 13, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Todos los movimientos</p>
            {filtered.length === 0 && (
              <div style={{ textAlign: "center", padding: "40px 0", color: "#3d3858" }}>
                <p style={{ margin: 0, fontSize: 14 }}>Sin movimientos este mes</p>
              </div>
            )}
            {filtered.map(t => (
              <div key={t.id} style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "14px 16px", background: "#13101e", borderRadius: 16, marginBottom: 8, border: "1px solid #1e1a30" }}>
                <div style={{ display: "flex", alignItems: "center", gap: 12 }}>
                  <div style={{ width: 10, height: 10, borderRadius: "50%", background: CAT_COLORS[t.category] || "#7c6af7", flexShrink: 0 }} />
                  <div>
                    <p style={{ margin: 0, fontSize: 13, fontWeight: 600, color: "#f1f0ff" }}>{t.category}</p>
                    <p style={{ margin: 0, fontSize: 11, color: "#6b6880" }}>{t.date}{t.note ? ` · ${t.note}` : ""}</p>
                  </div>
                </div>
                <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                  <p style={{ margin: 0, fontSize: 14, fontWeight: 700, color: t.type === "income" ? "#4ade80" : "#f87171" }}>
                    {t.type === "income" ? "+" : "-"}{formatCurrency(t.amount)}
                  </p>
                  <button onClick={() => deleteTransaction(t.id)} style={{ background: "none", border: "none", color: "#3d3858", cursor: "pointer", fontSize: 16, padding: 0 }}>×</button>
                </div>
              </div>
            ))}
          </div>
        )}

        {/* ADD FORM */}
        {tab === "add" && showForm && (
          <div>
            <p style={{ margin: "0 0 16px", fontSize: 13, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Nuevo movimiento</p>

            {/* Type toggle */}
            <div style={{ display: "flex", background: "#13101e", borderRadius: 14, padding: 4, gap: 4, marginBottom: 16 }}>
              {["expense","income"].map(type => (
                <button key={type} onClick={() => setForm(f => ({ ...f, type, category: type === "income" ? "Salario" : "Comida" }))}
                  style={{ flex: 1, padding: "12px 0", borderRadius: 10, border: "none", cursor: "pointer", fontSize: 13, fontWeight: 600, transition: "all .2s",
                    background: form.type === type ? (type === "income" ? "linear-gradient(135deg,#4ade80,#22c55e)" : "linear-gradient(135deg,#f87171,#ef4444)") : "transparent",
                    color: form.type === type ? "#fff" : "#6b6880" }}>
                  {type === "income" ? "↑ Ingreso" : "↓ Gasto"}
                </button>
              ))}
            </div>

            {/* Amount */}
            <div style={{ marginBottom: 12 }}>
              <p style={{ margin: "0 0 6px", fontSize: 11, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Monto</p>
              <input type="number" placeholder="0.00" value={form.amount} onChange={e => setForm(f => ({ ...f, amount: e.target.value }))}
                style={{ width: "100%", padding: "14px 16px", background: "#13101e", border: "1px solid #2a2545", borderRadius: 14, color: "#f1f0ff", fontSize: 20, fontWeight: 700, boxSizing: "border-box", outline: "none", fontFamily: "'Space Grotesk',sans-serif" }} />
            </div>

            {/* Category */}
            <div style={{ marginBottom: 12 }}>
              <p style={{ margin: "0 0 6px", fontSize: 11, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Categoría</p>
              <select value={form.category} onChange={e => setForm(f => ({ ...f, category: e.target.value }))}
                style={{ width: "100%", padding: "14px 16px", background: "#13101e", border: "1px solid #2a2545", borderRadius: 14, color: "#f1f0ff", fontSize: 14, boxSizing: "border-box", outline: "none", appearance: "none" }}>
                {CATEGORIES[form.type].map(c => <option key={c} value={c}>{c}</option>)}
              </select>
            </div>

            {/* Date */}
            <div style={{ marginBottom: 12 }}>
              <p style={{ margin: "0 0 6px", fontSize: 11, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Fecha</p>
              <input type="date" value={form.date} onChange={e => setForm(f => ({ ...f, date: e.target.value }))}
                style={{ width: "100%", padding: "14px 16px", background: "#13101e", border: "1px solid #2a2545", borderRadius: 14, color: "#f1f0ff", fontSize: 14, boxSizing: "border-box", outline: "none", colorScheme: "dark" }} />
            </div>

            {/* Note */}
            <div style={{ marginBottom: 20 }}>
              <p style={{ margin: "0 0 6px", fontSize: 11, color: "#6b6880", letterSpacing: 1, textTransform: "uppercase" }}>Nota (opcional)</p>
              <input type="text" placeholder="Descripción..." value={form.note} onChange={e => setForm(f => ({ ...f, note: e.target.value }))}
                style={{ width: "100%", padding: "14px 16px", background: "#13101e", border: "1px solid #2a2545", borderRadius: 14, color: "#f1f0ff", fontSize: 14, boxSizing: "border-box", outline: "none" }} />
            </div>

            <button onClick={addTransaction}
              style={{ width: "100%", padding: "16px 0", background: "linear-gradient(135deg,#7c6af7,#9f8fff)", border: "none", borderRadius: 16, color: "#fff", fontSize: 16, fontWeight: 700, cursor: "pointer", boxShadow: "0 4px 20px #7c6af750", letterSpacing: .5 }}>
              Guardar
            </button>
            <button onClick={() => { setShowForm(false); setTab("home"); }}
              style={{ width: "100%", padding: "14px 0", background: "none", border: "none", color: "#6b6880", fontSize: 14, cursor: "pointer", marginTop: 8 }}>
              Cancelar
            </button>
          </div>
        )}
      </div>
    </div>
  );
}
