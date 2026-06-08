import { useState } from "react";

const sections = [
  {
    id: "overview",
    emoji: "🗺️",
    title: "전체 개요",
    color: "#4F7FFA",
    content: {
      type: "map",
      items: [
        {
          label: "희소 표현",
          sub: "One-Hot Encoding",
          arrow: "→ 문제: 메모리 낭비, 의미 표현 X",
          color: "#e74c3c",
        },
        {
          label: "밀집 표현",
          sub: "Word Embedding",
          arrow: "→ 해결: 저차원 실수 벡터",
          color: "#27ae60",
        },
      ],
      methods: [
        { name: "Word2Vec", sub: "CBOW / Skip-Gram", tag: "★ 핵심" },
        { name: "FastText", sub: "Subword n-gram", tag: "OOV 해결" },
        { name: "Doc2Vec", sub: "DM / DBOW", tag: "문서 단위" },
      ],
    },
  },
  {
    id: "onehot",
    emoji: "❌",
    title: "One-Hot Encoding (희소 표현)",
    color: "#e74c3c",
    content: {
      type: "compare",
      bad: [
        "단어 10,000개 → 벡터 차원 10,000",
        "해당 단어 위치만 1, 나머지 9,999개 = 0",
        "메모리 낭비 심각",
        "단어 간 의미 유사도 계산 불가",
        "모든 단어 간 거리 동일",
      ],
      good: ["구현 단순", "이해 쉬움", "단어를 독립적으로 표현 가능"],
      example: 'Rome  = [1, 0, 0, ..., 0]\nParis = [0, 1, 0, ..., 0]\nItaly = [0, 0, 1, ..., 0]',
    },
  },
  {
    id: "embedding",
    emoji: "✅",
    title: "Word Embedding (밀집 표현)",
    color: "#27ae60",
    content: {
      type: "feature",
      desc: "원핫 벡터를 저차원 실수 벡터(Dense Vector)로 변환",
      features: [
        {
          icon: "📦",
          title: "효율적 연산",
          desc: "차원 축소로 공간·시간 비용 절감",
        },
        {
          icon: "🔍",
          title: "의미적 유사도",
          desc: "학습 목적에 맞게 단어 간 거리 생성",
        },
        {
          icon: "➕",
          title: "단어 간 연산",
          desc: "한국 - 서울 + 도쿄 = 일본",
        },
        {
          icon: "🔄",
          title: "전이학습",
          desc: "학습된 가중치 행렬을 다른 태스크에 재사용",
        },
      ],
      example: '강아지 = [0.2, 1.8, 1.1, -2.1, 1.1, 2.8, ...]',
    },
  },
  {
    id: "word2vec",
    emoji: "🧠",
    title: "Word2Vec",
    color: "#8e44ad",
    content: {
      type: "word2vec",
      principle: "분포가설: 비슷한 문맥에 등장하는 단어 → 비슷한 의미",
      models: [
        {
          name: "CBOW",
          full: "Continuous Bag of Words",
          desc: "주변 단어 → 중심 단어 예측",
          flow: ["주변단어 원핫벡터 입력", "×W → 임베딩벡터 생성", "평균 → 중심단어 벡터 v", "×W′ → softmax → 예측"],
          note: "윈도우 크기 n → 앞뒤 2n개 단어 참조",
        },
        {
          name: "Skip-Gram",
          full: "Skip-Gram",
          desc: "중심 단어 → 주변 단어 예측",
          flow: ["중심단어 원핫벡터 입력", "×W → 임베딩벡터", "×W′ → 주변단어들 예측"],
          note: "일반적으로 CBOW보다 성능 우수 ★",
        },
      ],
      network: "은닉층 1개 Shallow Neural Network\n투사층(Projection Layer): 활성화 함수 없음\nLoss: Cross Entropy → Backpropagation",
      negative: "Negative Sampling: 전체 V에 softmax 대신\n이진분류(이 단어가 중심단어인가?)로 연산량 감소",
    },
  },
  {
    id: "fasttext",
    emoji: "⚡",
    title: "FastText",
    color: "#e67e22",
    content: {
      type: "fasttext",
      problem: "Word2Vec의 한계: OOV(Out Of Vocabulary) 단어에 취약, 형태학적 특징 미반영",
      solution: "서브워드(Subword) n-gram으로 단어를 분해하여 표현",
      example: {
        word: "Orange → <Orange>",
        ngrams: [
          { n: "2-gram", items: "<O, Or, ra, an, ng, ge, e>" },
          { n: "3-gram", items: "<Or, Ora, ran, ang, nge, ge>" },
          { n: "4-gram", items: "<Ora, Oran, rang, ange, nge>" },
        ],
        formula: "v(Orange) = 모든 n-gram 벡터의 합",
      },
      oov: "Oranges가 없어도 Orange의 subword를 공유 → 벡터 생성 가능",
      perf: "sisg(FastText) > sisg-(OOV미해결) > cbow(Word2Vec)",
    },
  },
  {
    id: "doc2vec",
    emoji: "📄",
    title: "Doc2Vec",
    color: "#16a085",
    content: {
      type: "doc2vec",
      base: "Word2Vec을 문서(Document) 단위로 확장",
      how: "문서 ID를 단어들과 함께 학습 → 문서 자체의 의미 벡터 생성",
      models: [
        {
          name: "DM",
          full: "Distributed Memory",
          desc: "문서 벡터 + 주변단어 → 중심단어 예측 (CBOW 유사)",
        },
        {
          name: "DBOW",
          full: "Distributed Bag of Words",
          desc: "문서 벡터만으로 → 문서 내 단어들 예측 (Skip-Gram 유사)",
        },
      ],
      uses: ["문서 분류", "문서 추천", "유사 문서 검색", "감성 분석"],
    },
  },
  {
    id: "compare",
    emoji: "📊",
    title: "모델 비교 총정리",
    color: "#2c3e50",
    content: {
      type: "table",
      rows: [
        { model: "One-Hot", unit: "단어", dim: "V (매우 큼)", oov: "❌", semantic: "❌", transfer: "❌" },
        { model: "CBOW", unit: "단어", dim: "M (설정)", oov: "❌", semantic: "✅", transfer: "✅" },
        { model: "Skip-Gram", unit: "단어", dim: "M (설정)", oov: "❌", semantic: "✅✅", transfer: "✅" },
        { model: "FastText", unit: "서브워드", dim: "M (설정)", oov: "✅", semantic: "✅✅", transfer: "✅" },
        { model: "Doc2Vec", unit: "문서", dim: "M (설정)", oov: "△", semantic: "✅✅", transfer: "✅" },
      ],
    },
  },
];

function OverviewSection({ content }) {
  return (
    <div>
      <div style={{ display: "flex", gap: 16, marginBottom: 20, flexWrap: "wrap" }}>
        {content.items.map((item) => (
          <div
            key={item.label}
            style={{
              flex: 1,
              minWidth: 200,
              padding: "14px 18px",
              borderRadius: 10,
              border: `2px solid ${item.color}`,
              background: item.color + "11",
            }}
          >
            <div style={{ fontWeight: 700, color: item.color, fontSize: 15 }}>{item.label}</div>
            <div style={{ fontSize: 12, color: "#888", marginBottom: 4 }}>{item.sub}</div>
            <div style={{ fontSize: 13, color: "#555" }}>{item.arrow}</div>
          </div>
        ))}
      </div>
      <div style={{ fontWeight: 600, marginBottom: 10, color: "#444" }}>주요 임베딩 기법</div>
      <div style={{ display: "flex", gap: 10, flexWrap: "wrap" }}>
        {content.methods.map((m) => (
          <div
            key={m.name}
            style={{
              padding: "10px 16px",
              borderRadius: 8,
              background: "#f0f4ff",
              border: "1.5px solid #4F7FFA",
              flex: 1,
              minWidth: 120,
              textAlign: "center",
            }}
          >
            <div style={{ fontWeight: 700, color: "#4F7FFA", fontSize: 14 }}>{m.name}</div>
            <div style={{ fontSize: 12, color: "#666" }}>{m.sub}</div>
            <div
              style={{
                marginTop: 6,
                fontSize: 11,
                background: "#4F7FFA",
                color: "#fff",
                borderRadius: 4,
                padding: "2px 6px",
                display: "inline-block",
              }}
            >
              {m.tag}
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

function CompareSection({ content }) {
  return (
    <div>
      <div style={{ display: "flex", gap: 16, marginBottom: 16, flexWrap: "wrap" }}>
        <div style={{ flex: 1, minWidth: 180 }}>
          <div style={{ fontWeight: 700, color: "#e74c3c", marginBottom: 8 }}>❌ 단점</div>
          {content.bad.map((b, i) => (
            <div
              key={i}
              style={{ fontSize: 13, padding: "5px 0", borderBottom: "1px solid #fdd", color: "#555" }}
            >
              • {b}
            </div>
          ))}
        </div>
        <div style={{ flex: 1, minWidth: 180 }}>
          <div style={{ fontWeight: 700, color: "#27ae60", marginBottom: 8 }}>✅ 장점</div>
          {content.good.map((g, i) => (
            <div
              key={i}
              style={{ fontSize: 13, padding: "5px 0", borderBottom: "1px solid #dfd", color: "#555" }}
            >
              • {g}
            </div>
          ))}
        </div>
      </div>
      <div
        style={{
          background: "#1e1e2e",
          color: "#a8d8ea",
          borderRadius: 8,
          padding: "12px 16px",
          fontFamily: "monospace",
          fontSize: 13,
          lineHeight: 1.7,
          whiteSpace: "pre",
        }}
      >
        {content.example}
      </div>
    </div>
  );
}

function FeatureSection({ content }) {
  return (
    <div>
      <div
        style={{
          background: "#eafaf1",
          border: "1.5px solid #27ae60",
          borderRadius: 8,
          padding: "10px 14px",
          marginBottom: 16,
          fontSize: 14,
          color: "#1e8449",
          fontWeight: 600,
        }}
      >
        {content.desc}
      </div>
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12, marginBottom: 16 }}>
        {content.features.map((f) => (
          <div
            key={f.title}
            style={{ background: "#f9f9f9", borderRadius: 8, padding: "12px 14px", border: "1px solid #eee" }}
          >
            <div style={{ fontSize: 18, marginBottom: 4 }}>{f.icon}</div>
            <div style={{ fontWeight: 700, fontSize: 13, marginBottom: 4 }}>{f.title}</div>
            <div style={{ fontSize: 12, color: "#666" }}>{f.desc}</div>
          </div>
        ))}
      </div>
      <div
        style={{
          background: "#1e1e2e",
          color: "#a8d8ea",
          borderRadius: 8,
          padding: "10px 14px",
          fontFamily: "monospace",
          fontSize: 13,
        }}
      >
        {content.example}
      </div>
    </div>
  );
}

function Word2VecSection({ content }) {
  const [active, setActive] = useState(0);
  const m = content.models[active];
  return (
    <div>
      <div
        style={{
          background: "#f3e5f5",
          border: "1.5px solid #8e44ad",
          borderRadius: 8,
          padding: "10px 14px",
          marginBottom: 16,
          fontSize: 13,
          color: "#6c3483",
        }}
      >
        💡 <strong>핵심 원리:</strong> {content.principle}
      </div>
      <div style={{ display: "flex", gap: 8, marginBottom: 16 }}>
        {content.models.map((mod, i) => (
          <button
            key={mod.name}
            onClick={() => setActive(i)}
            style={{
              flex: 1,
              padding: "10px",
              borderRadius: 8,
              border: active === i ? "2px solid #8e44ad" : "2px solid #ddd",
              background: active === i ? "#8e44ad" : "#fff",
              color: active === i ? "#fff" : "#333",
              fontWeight: 700,
              cursor: "pointer",
              fontSize: 14,
            }}
          >
            {mod.name}
          </button>
        ))}
      </div>
      <div style={{ background: "#faf5ff", borderRadius: 10, padding: "14px 16px", marginBottom: 14 }}>
        <div style={{ fontWeight: 700, color: "#8e44ad", marginBottom: 6 }}>
          {m.name} — {m.full}
        </div>
        <div style={{ fontSize: 13, color: "#555", marginBottom: 10 }}>{m.desc}</div>
        <div style={{ display: "flex", alignItems: "center", gap: 6, flexWrap: "wrap" }}>
          {m.flow.map((step, i) => (
            <div key={i} style={{ display: "flex", alignItems: "center", gap: 6 }}>
              <div
                style={{
                  background: "#8e44ad",
                  color: "#fff",
                  borderRadius: 6,
                  padding: "5px 10px",
                  fontSize: 12,
                  fontWeight: 600,
                }}
              >
                {step}
              </div>
              {i < m.flow.length - 1 && <span style={{ color: "#8e44ad", fontWeight: 700 }}>→</span>}
            </div>
          ))}
        </div>
        <div
          style={{
            marginTop: 10,
            fontSize: 12,
            color: "#6c3483",
            background: "#e8d5f5",
            borderRadius: 6,
            padding: "6px 10px",
          }}
        >
          📌 {m.note}
        </div>
      </div>
      <div
        style={{
          background: "#1e1e2e",
          color: "#c9d1d9",
          borderRadius: 8,
          padding: "10px 14px",
          fontFamily: "monospace",
          fontSize: 12,
          lineHeight: 1.7,
          whiteSpace: "pre-wrap",
          marginBottom: 10,
        }}
      >
        {content.network}
      </div>
      <div
        style={{
          background: "#fff8e1",
          border: "1.5px solid #f39c12",
          borderRadius: 8,
          padding: "10px 14px",
          fontSize: 12,
          color: "#7d6608",
          whiteSpace: "pre-wrap",
        }}
      >
        ⚡ <strong>Negative Sampling:</strong> {"\n"}{content.negative.split(": ")[1]}
      </div>
    </div>
  );
}

function FastTextSection({ content }) {
  return (
    <div>
      <div
        style={{
          background: "#fef5e7",
          border: "1.5px solid #e67e22",
          borderRadius: 8,
          padding: "10px 14px",
          marginBottom: 12,
          fontSize: 13,
          color: "#784212",
        }}
      >
        ⚠️ <strong>Word2Vec 한계:</strong> {content.problem}
      </div>
      <div
        style={{
          background: "#eafaf1",
          border: "1.5px solid #27ae60",
          borderRadius: 8,
          padding: "10px 14px",
          marginBottom: 14,
          fontSize: 13,
          color: "#1e8449",
        }}
      >
        ✅ <strong>해결책:</strong> {content.solution}
      </div>
      <div style={{ marginBottom: 14 }}>
        <div style={{ fontWeight: 700, marginBottom: 8, fontSize: 13 }}>
          예시: <code style={{ background: "#f0f0f0", padding: "2px 6px", borderRadius: 4 }}>{content.example.word}</code>
        </div>
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
          {content.example.ngrams.map((ng) => (
            <div
              key={ng.n}
              style={{
                flex: 1,
                minWidth: 130,
                background: "#fff3e0",
                border: "1.5px solid #e67e22",
                borderRadius: 8,
                padding: "10px",
              }}
            >
              <div style={{ fontWeight: 700, fontSize: 12, color: "#e67e22", marginBottom: 4 }}>{ng.n}</div>
              <div style={{ fontSize: 11, color: "#666", fontFamily: "monospace" }}>{ng.items}</div>
            </div>
          ))}
        </div>
        <div
          style={{
            marginTop: 10,
            background: "#1e1e2e",
            color: "#a8d8ea",
            borderRadius: 8,
            padding: "8px 12px",
            fontFamily: "monospace",
            fontSize: 13,
          }}
        >
          {content.example.formula}
        </div>
      </div>
      <div
        style={{
          background: "#d5f5e3",
          border: "1.5px solid #27ae60",
          borderRadius: 8,
          padding: "10px 14px",
          fontSize: 13,
          color: "#1e8449",
          marginBottom: 10,
        }}
      >
        🔑 <strong>OOV 해결:</strong> {content.oov}
      </div>
      <div
        style={{
          background: "#eaf0fb",
          border: "1.5px solid #4F7FFA",
          borderRadius: 8,
          padding: "10px 14px",
          fontSize: 13,
          color: "#1a3a8f",
        }}
      >
        📊 <strong>성능:</strong> {content.perf}
      </div>
    </div>
  );
}

function Doc2VecSection({ content }) {
  return (
    <div>
      <div
        style={{
          background: "#e8f8f5",
          border: "1.5px solid #16a085",
          borderRadius: 8,
          padding: "10px 14px",
          marginBottom: 12,
          fontSize: 13,
          color: "#0e6655",
        }}
      >
        🔗 <strong>기반:</strong> {content.base}
      </div>
      <div
        style={{
          background: "#f0fafa",
          borderRadius: 8,
          padding: "10px 14px",
          marginBottom: 14,
          fontSize: 13,
          color: "#555",
          border: "1px solid #d0eeea",
        }}
      >
        <strong>동작:</strong> {content.how}
      </div>
      <div style={{ display: "flex", gap: 12, marginBottom: 14, flexWrap: "wrap" }}>
        {content.models.map((m) => (
          <div
            key={m.name}
            style={{
              flex: 1,
              minWidth: 200,
              background: "#f0fafa",
              border: "1.5px solid #16a085",
              borderRadius: 10,
              padding: "12px 14px",
            }}
          >
            <div style={{ fontWeight: 700, color: "#16a085", fontSize: 15 }}>{m.name}</div>
            <div style={{ fontSize: 12, color: "#888", marginBottom: 6 }}>{m.full}</div>
            <div style={{ fontSize: 13, color: "#555" }}>{m.desc}</div>
          </div>
        ))}
      </div>
      <div>
        <div style={{ fontWeight: 700, marginBottom: 8, color: "#16a085" }}>📌 활용 분야</div>
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
          {content.uses.map((u) => (
            <div
              key={u}
              style={{
                background: "#16a085",
                color: "#fff",
                borderRadius: 20,
                padding: "6px 14px",
                fontSize: 13,
                fontWeight: 600,
              }}
            >
              {u}
            </div>
          ))}
        </div>
      </div>
    </div>
  );
}

function TableSection({ content }) {
  const headers = ["모델", "단위", "차원", "OOV", "의미유사도", "전이학습"];
  const keys = ["model", "unit", "dim", "oov", "semantic", "transfer"];
  return (
    <div style={{ overflowX: "auto" }}>
      <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 13 }}>
        <thead>
          <tr style={{ background: "#2c3e50", color: "#fff" }}>
            {headers.map((h) => (
              <th key={h} style={{ padding: "10px 12px", textAlign: "center", fontWeight: 700 }}>
                {h}
              </th>
            ))}
          </tr>
        </thead>
        <tbody>
          {content.rows.map((row, i) => (
            <tr
              key={row.model}
              style={{ background: i % 2 === 0 ? "#f9f9f9" : "#fff", borderBottom: "1px solid #eee" }}
            >
              {keys.map((k) => (
                <td
                  key={k}
                  style={{
                    padding: "10px 12px",
                    textAlign: "center",
                    fontWeight: k === "model" ? 700 : 400,
                    color:
                      k === "model"
                        ? "#2c3e50"
                        : String(row[k]).includes("❌")
                        ? "#e74c3c"
                        : String(row[k]).includes("✅")
                        ? "#27ae60"
                        : "#555",
                  }}
                >
                  {row[k]}
                </td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

function SectionContent({ section }) {
  const { content } = section;
  switch (content.type) {
    case "map":
      return <OverviewSection content={content} />;
    case "compare":
      return <CompareSection content={content} />;
    case "feature":
      return <FeatureSection content={content} />;
    case "word2vec":
      return <Word2VecSection content={content} />;
    case "fasttext":
      return <FastTextSection content={content} />;
    case "doc2vec":
      return <Doc2VecSection content={content} />;
    case "table":
      return <TableSection content={content} />;
    default:
      return null;
  }
}

export default function App() {
  const [active, setActive] = useState(0);
  const sec = sections[active];

  return (
    <div
      style={{
        fontFamily: "'Noto Sans KR', 'Apple SD Gothic Neo', sans-serif",
        minHeight: "100vh",
        background: "#f4f6fb",
        display: "flex",
        flexDirection: "column",
      }}
    >
      {/* Header */}
      <div
        style={{
          background: "#1a2340",
          color: "#fff",
          padding: "18px 24px 14px",
          display: "flex",
          alignItems: "center",
          gap: 12,
        }}
      >
        <div style={{ fontSize: 22, fontWeight: 900, letterSpacing: -1 }}>📚 워드임베딩 시험노트</div>
        <div style={{ marginLeft: "auto", fontSize: 12, color: "#aab", background: "#2a3555", borderRadius: 6, padding: "4px 10px" }}>
          자연어 처리 · 2026
        </div>
      </div>

      {/* Tab Nav */}
      <div
        style={{
          display: "flex",
          gap: 4,
          padding: "10px 12px",
          background: "#fff",
          borderBottom: "2px solid #eee",
          overflowX: "auto",
          flexWrap: "wrap",
        }}
      >
        {sections.map((s, i) => (
          <button
            key={s.id}
            onClick={() => setActive(i)}
            style={{
              padding: "7px 14px",
              borderRadius: 20,
              border: active === i ? `2px solid ${s.color}` : "2px solid transparent",
              background: active === i ? s.color : "#f0f0f0",
              color: active === i ? "#fff" : "#555",
              fontWeight: active === i ? 700 : 500,
              cursor: "pointer",
              fontSize: 13,
              whiteSpace: "nowrap",
              transition: "all 0.15s",
            }}
          >
            {s.emoji} {s.title}
          </button>
        ))}
      </div>

      {/* Content */}
      <div style={{ flex: 1, padding: "20px 16px", maxWidth: 800, width: "100%", margin: "0 auto" }}>
        <div
          style={{
            background: "#fff",
            borderRadius: 14,
            boxShadow: "0 2px 12px rgba(0,0,0,0.07)",
            overflow: "hidden",
          }}
        >
          <div
            style={{
              background: sec.color,
              color: "#fff",
              padding: "16px 20px",
              fontSize: 18,
              fontWeight: 800,
              display: "flex",
              alignItems: "center",
              gap: 10,
            }}
          >
            <span style={{ fontSize: 22 }}>{sec.emoji}</span>
            {sec.title}
          </div>
          <div style={{ padding: "20px" }}>
            <SectionContent section={sec} />
          </div>
        </div>
      </div>

      {/* Footer nav */}
      <div
        style={{
          display: "flex",
          justifyContent: "space-between",
          padding: "12px 20px",
          background: "#fff",
          borderTop: "1px solid #eee",
        }}
      >
        <button
          onClick={() => setActive((p) => Math.max(0, p - 1))}
          disabled={active === 0}
          style={{
            padding: "8px 18px",
            borderRadius: 8,
            border: "1.5px solid #ccc",
            background: active === 0 ? "#f5f5f5" : "#fff",
            color: active === 0 ? "#ccc" : "#333",
            cursor: active === 0 ? "not-allowed" : "pointer",
            fontWeight: 600,
            fontSize: 13,
          }}
        >
          ← 이전
        </button>
        <span style={{ fontSize: 13, color: "#888", alignSelf: "center" }}>
          {active + 1} / {sections.length}
        </span>
        <button
          onClick={() => setActive((p) => Math.min(sections.length - 1, p + 1))}
          disabled={active === sections.length - 1}
          style={{
            padding: "8px 18px",
            borderRadius: 8,
            border: "1.5px solid #ccc",
            background: active === sections.length - 1 ? "#f5f5f5" : "#fff",
            color: active === sections.length - 1 ? "#ccc" : "#333",
            cursor: active === sections.length - 1 ? "not-allowed" : "pointer",
            fontWeight: 600,
            fontSize: 13,
          }}
        >
          다음 →
        </button>
      </div>
    </div>
  );
}
