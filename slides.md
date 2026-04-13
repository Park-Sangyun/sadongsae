---
theme: default
class: text-center
highlighter: shiki
lineNumbers: true
drawings:
  persist: false
transition: slide-left
title: AI 가속기의 종류 - GPU, NPU, LPU
---

# AI 가속기의 종류
## 목적에 따른 아키텍처의 분화: GPU, NPU, LPU

<div class="pt-12">
  <span class="opacity-50 text-sm">박상윤</span>
</div>

---
layout: default
---

# 1. AI 가속기(AI Accelerator)란?
### 딥러닝 연산에 최적화된 특수 목적 하드웨어

- 대규모 행렬 곱셈 등 인공지능에 필요한 방대한 연산을 고속으로 처리하는데 사용되는 하드웨어 시스템
- 범용적인 CPU는 복잡한 제어 로직을 갖춰 단순 반복적인 병렬 연산 효율이 낮음
- **AI 가속기의 핵심 목표**
  - **연산 처리량(Throughput)** 극대화
  - **전력 대비 성능(Efficiency)** 최적화
  - **응답 지연 시간(Latency)** 최소화

---
layout: default
---

# 2. 하드웨어 분화
### 모델의 특성과 서비스 목적에 따른 아키텍처 선택

- **과거:** GPU 하나로 학습부터 추론까지 모든 과정 수행 (범용성 중심)
- **현재:** 하드웨어의 물리적 한계를 극복하기 위해 '전문화'된 칩 도입

<div class="grid grid-cols-3 gap-4 mt-10">
  <div class="p-4 border border-blue-500/30 bg-blue-500/5 rounded">
    <h3 class="text-blue-400">GPU</h3>
    <p class="text-xs">범용 병렬 연산<br>학습 단계의 표준</p>
  </div>
  <div class="p-4 border border-green-500/30 bg-green-500/5 rounded">
    <h3 class="text-green-400">NPU (TPU)</h3>
    <p class="text-xs">신경망 연산 특화<br>최고의 전성비</p>
  </div>
  <div class="p-4 border border-orange-500/30 bg-orange-500/5 rounded">
    <h3 class="text-orange-400">LPU</h3>
    <p class="text-xs">LLM 추론 특화<br>극저지연 속도</p>
  </div>
</div>

---
layout: two-cols
---

<h1 class="text-[32px] font-bold whitespace-nowrap tracking-tight">3. GPU (Graphics Processing Unit)</h1>
<h3 class="mt-2 text-[20px] text-gray-400">범용 병렬 연산</h3>

- **설계 철학의 차이:**
  - **CPU:** 소수 정예 코어로 복잡한 제어 로직과 지연 시간 최소화에 집중
  - **GPU:** 수만 개의 단순 연산 유닛(ALU)을 통해 데이터 처리량 극대화
- **AI와의 시너지:**
  - 딥러닝 연산의 90%를 차지하는 '행렬 곱셈'은 각 원소의 독립성이 보장됨
  - GPU의 대규모 병렬 처리 구조는 이러한 행렬 연산을 동시에 처리하는 데 완벽하게 부합함

::right::

<div class="ml-6 mt-16 flex flex-col justify-center h-full space-y-4">
  <div class="bg-white/5 p-3 rounded-lg border border-white/10">
    <div class="text-[12px] font-bold mb-1 text-orange-400 text-center">CPU: 직렬 처리 (Serial)</div>
    <img src="/cpu.gif" class="w-full h-32 object-contain rounded shadow-md" />
  </div>

  <div class="bg-white/5 p-3 rounded-lg border border-white/10">
    <div class="text-[12px] font-bold mb-1 text-blue-400 text-center">GPU: 병렬 처리 (Parallel)</div>
    <img src="/gpu.gif" class="w-full h-32 object-contain rounded shadow-md" />
  </div>

  <p class="text-[10px] opacity-50 text-center italic mt-2">
    "단일 작업의 정교함(CPU) vs 대량 데이터의 동시성(GPU)"
  </p>
</div>

---
layout: two-cols
---

# 3.1 GPU의 진화: NVIDIA
### AI 가속기를 품은 범용 칩

- **하드웨어의 진화: 텐서 코어 (Tensor Core)**
  - 그래픽 연산용 코어 외에, AI의 **행렬 곱셈(MAC)만을 1클럭에 처리**하는 전용 유닛을 칩 내부에 탑재
  - 칩 안에 AI 전용 칩을 내장한 구조로 진화

::right::

<div class="ml-4 flex flex-col items-center justify-center h-full">
  <img src="/tensor-core.png" class="w-full h-64 object-contain rounded-lg shadow-lg border border-white/10 bg-white/5 p-2" alt="NVIDIA Tensor Core and CUDA" />
</div>

---
layout: two-cols
---

# 4. NPU (Neural Processing Unit)
### 온디바이스 AI와 전력 효율의 극대화

- **핵심 개념:** 신경망 연산(MAC)에만 집중하여 전력 대비 성능(전성비)을 극대화한 특수 목적 칩
- **온디바이스(On-Device) AI의 심장:** 배터리와 발열 한계가 있는 기기에서 필수적
  - **Apple:** M시리즈 및 A시리즈의 'Neural Engine'
  - **Qualcomm:** 스냅드래곤(Snapdragon)의 'Hexagon NPU'
  - **Samsung:** 엑시노스(Exynos) NPU
- **AI 반도체 스타트업의 약진:**
  - **퓨리오사AI (FuriosaAI):** 뛰어난 전력 효율과 추론 성능을 자랑하는 국산 NPU 가속기

::right::

<div class="ml-4 flex flex-col items-center justify-center h-full">
  <img src="/npu-mobile.png" class="w-full h-64 object-contain rounded-lg shadow-lg border border-white/10 bg-white/5 p-2" alt="Mobile NPU and FuriosaAI" />
  <p class="text-[10px] mt-3 opacity-50 text-center italic">"M4칩 Neural Engine"</p>
</div>

---
layout: two-cols
---

<h1 class="text-[32px] font-bold whitespace-nowrap tracking-tight">4.1 TPU (Tensor Processing Unit)</h1>
<h3 class="mt-2 text-[20px] text-gray-400">구글의 클라우드 스케일 AI 가속기</h3>

- **시스톨릭 어레이 (Systolic Array) 아키텍처**
  - 데이터가 연산기 사이를 **물결처럼 흐르며 연속 계산**되는 구조
  - 메모리 접근(병목)을 최소화하여 연산 효율 극대화
- **핵심 연산기: MXU (Matrix Multiply Unit)**
  - 딥러닝 전용 행렬 곱셈을 한 클럭에 수천 개씩 동시 처리
- **초거대 스케일 확장 (Pod)**
  - 고속 네트워크(ICI) 내장으로 수천 개의 칩을 하나처럼 연결
  - 거대 언어 모델(LLM) 학습 및 서비스에 최적화

::right::

<div class="ml-6 mt-12 flex flex-col justify-center h-full space-y-4">
  <div class="bg-white/5 p-2 rounded-lg border border-white/10">
    <div class="text-[11px] font-bold mb-1 text-green-400 text-center">메모리에서 연산기로 데이터 로드</div>
    <img src="/tpu-1.gif" class="w-full h-28 object-contain rounded shadow-md bg-white" />
  </div>

  <div class="bg-white/5 p-2 rounded-lg border border-white/10">
    <div class="text-[11px] font-bold mb-1 text-blue-400 text-center">Systolic Array 데이터 흐름 연산</div>
    <img src="/tpu-2.gif" class="w-full h-28 object-contain rounded shadow-md bg-white" />
  </div>
</div>

---
layout: two-cols
---

<h1 class="text-[32px] font-bold whitespace-nowrap tracking-tight">5. LPU (Language Processing Unit)</h1>

- **핵심 특징: SRAM 기반 On-Chip 아키텍처**
  - **DRAM(HBM) 제거:** 데이터 리프레시와 물리적 이동 시간을 유발하는 외장 메모리 완전 배제
  - **초고속 데이터 공급:** 연산기 옆에 찰싹 붙은 SRAM이 0에 가까운 지연 시간으로 데이터 공급
- **설계 철학: 결정론적(Deterministic) 흐름**
  - 모든 연산 경로를 컴파일 단계에서 확정하여 칩 내부의 '교통 체증'을 물리적으로 방지
- **장점:** - 실시간 대화가 가능한 압도적 추론 속도 (GPU 대비 수십 배)
- **단점:** - **낮은 집적도:** SRAM의 물리적 한계로 칩당 메모리 용량이 매우 작음 (약 230MB)
  - **고비용/저용량:** 모델 하나 구동에 수백 개의 칩이 필요하여 시스템 구축 단가가 높음

::right::

<div class="ml-6 mt-16 flex flex-col justify-center h-full space-y-4">
  <div class="bg-white/5 p-3 rounded-lg border border-white/10 text-center">
    <div class="text-[12px] font-bold mb-2 text-orange-400">LPU 아키텍처 및 데이터 흐름</div>
    <img src="/lpu.png" class="w-full h-52 object-contain rounded shadow-md bg-white/5" alt="Groq LPU Architecture" />
  </div>
</div>

---
layout: center
---

# 요약: AI 가속기 비교

| 구분 | GPU (범용) | NPU / TPU (효율) | LPU (속도) |
| :--- | :--- | :--- | :--- |
| **설계 목표** | 범용 병렬 처리 | 전성비 및 연산 최적화 | **극단의 추론 지연 시간 단축** |
| **핵심 메모리** | HBM (외장) | HBM + DRAM | **Full SRAM (내장)** |
| **주요 활용** | 모든 AI 모델 학습 | 모바일 AI, Gemini 가속 | 실시간 LLM 추론 서비스 |
| **한계점** | 높은 전력 소모 | 모델 구조 변화에 취약 | 작은 메모리 용량 |

---
layout: center
class: text-center
---

# 감사합니다
