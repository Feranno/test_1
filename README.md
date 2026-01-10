# Building an 8-Bit Computer From Scratch
(conditional_jump_program.mp4)

I spent 6 hours debugging a computer I built from scratch, only to discover the problem was one loose wire.

Last year, I built an 8-bit computer using breadboards, logic gates, and 200+ hand-wired connections. No CPU, no microprocessor—just transistors and determination.

The reality: I spent 2-3x longer debugging than building. I wanted to quit 70+ times. Power distribution problems looked like logic bugs. Messy wiring turned debugging into archaeology.

But here's what I didn't expect to learn: the same debugging principles apply everywhere. Check infrastructure before logic. Respect component limits. Clean code (or clean wiring) pays for itself 10x over.

Now I'm building a GPU in Verilog, applying these lessons to understand ML systems architecture from first principles.

#FirstPrinciples #TechnicalLearning #ComputerArchitecture

---

## About This Writeup

**I'd like to thank** Mr. Wang, Charles Petzold, Ben Eater, and my dad for inspiration.

**tl;dr:** Stop presenting projects as "look what I built" and start presenting them as "here's how I think and learn." The computer is just evidence. Your thought process is the product.

### Who is this writeup for?

- Startup founders/engineers who value first-principles thinking
- People who want to understand the "why" behind abstractions, not just the "how"
- Anyone tired of surface-level tutorials and ready to build real understanding through pain

If you're looking for "10 tips to understand computers," this isn't it. If you want to see what it actually looks like to learn something deeply—including the 70+ moments I wanted to quit—read on.

---

## Why I Did This

Back in my digital electronics class in high school, our class divided into teams to learn and play with designing digital logic circuits. I remember my teacher at the time gave us a book to read called *Code: The Hidden Language of Computer Hardware and Software*. Since then, I've wanted to understand how computers actually work—not just use them, but make sense of what seemed like black boxes to me.

---

## What I Built

An 8-bit computer from breadboards and logic gates—no microprocessors, no pre-built CPU. Following the SAP-1 (Simple As Possible) architecture, I wired together ~200 connections by hand to create something that can store and execute programs.

### What makes something "a computer"

Just six essential components:
- **Memory** (16 bytes)
- **ALU** (add/subtract)
- **Control unit** (coordinates everything)
- **Program counter** (tracks position in program)
- **Clock** (synchronizes operations)
- **I/O** (7-segment displays)

That's it. Everything else—operating systems, compilers, GUIs—are layers built on top.

### The constraints

- 16 instructions per program maximum
- 8-bit operations (numbers from 0-255)
- No multiplication/division in hardware (must be programmed)
- ~500 Hz clock speed (billions of times slower than modern CPUs)
- Binary input only—you program it by setting switches

Yet it's **Turing complete**: Can compute anything a modern computer can (theoretically). I've run programs for Fibonacci sequences, prime checking, and conditional loops. The Apollo Guidance Computer that landed humans on the moon wasn't fundamentally different—just more refined.

### Why physical over simulation

Every wire you place teaches you something. Power distribution isn't abstract—you see which breadboards aren't getting voltage. Race conditions aren't theoretical—you watch the clock signals arrive out of sync. When it breaks (and it will), you can't just recompile—you have to think through every layer simultaneously.

Sounds simple, right? It wasn't.

---

## The Reality

I spent 2-3x longer debugging than building. Not exaggerating—for every hour placing wires, I spent 2-3 hours figuring out why things didn't work. I wanted to quit at least 70 times.

### The debugging process

Work for 2-3 hours, get nowhere, get frustrated, walk away. Come back the next day with fresh eyes and find the issue in 15 minutes. This pattern repeated for weeks.

### Why I kept going

Sunk cost fallacy at first, honestly. But eventually it became about proving to myself I could finish something this frustrating. Every time I wanted to quit, I'd think: "Just one more bug. If I can't fix it after that, I'll stop." Then I'd fix it and there'd be another one.

---

## What Broke

### Power distribution failures
I'd spend hours debugging logic only to discover a chip wasn't getting power. Now I check infrastructure first. In software: verify the database is running before debugging the query.

### Burnt LEDs
Skipped current-limiting resistors thinking "it'll probably work." It didn't. Learned to respect component limits. In software: load test before launch, not after the crash.

### Wiring nightmares
Messy wiring turned every bug into a multi-hour archaeology expedition. Clean wiring paid for itself 10x over. In software: readable code is faster to debug than clever code.

### Worst debugging moment

Spent 6 hours tracking down why the ALU would randomly output garbage. Checked every logic gate. Rewired connections. Wrote test programs. Finally discovered: one of the EEPROM address lines was intermittent due to a loose wire. One wire. Six hours. This is why I now test infrastructure before debugging logic.

But the technical debugging wasn't the real lesson.

---

## What I Learned

The breadboard computer gave me intuitions I couldn't get from Verilog alone:

- Physical debugging forces you to think about failure modes at every layer simultaneously (power, logic, timing, wiring)
- When you can't "console.log" your way through problems, you develop better mental models upfront
- The constraint of 16 instructions teaches you to write efficient code in ways that unlimited memory never does

**Would I recommend building one?** No—the ROI is terrible if you just want to learn computer architecture. But if you want to develop intuition for how abstraction layers hide complexity (and their costs), it's invaluable.

That's why my next project is in Verilog—I have the physical intuition now, so I can iterate 1000x faster.

---

## Why This Matters: From Toys to Operating Systems

The wild thing about computer architecture: Margaret Hamilton in the 1960s looked at systems not much more capable than what I built and envisioned operating systems, time-sharing, interpreters.

This is the startup mindset—seeing the toy and imagining the future. Every transformative product started as something limited:
- **First web browsers:** could barely render text
- **First smartphones:** worse than existing phones + worse than existing PDAs
- **First LLMs:** could barely complete sentences

The people who built those things didn't see limitations—they saw scaffolding for what could exist. That's what this project taught me to look for: not what is, but what could be with the right next layer of abstraction.

---

## What's Next

I'm building a tiny-gpu in Verilog to understand GPU architecture from first principles. After building the breadboard computer, I know what questions to ask:
- Where are the bottlenecks? (Memory bandwidth, not compute)
- What's the minimal viable architecture? (Parallel execution units + shared memory)
- What abstractions are essential vs. nice-to-have? (SIMD is essential, cache coherency can come later)

The goal isn't to build a production GPU—it's to develop intuition for why GPUs are designed the way they are, so I can reason about ML systems performance and make better architectural decisions.

The pattern continues: build it small, understand the constraints, then scale up. Whether that's distributed systems, ML infrastructure, or embedded systems—the approach stays the same.

---

## The Final Build

![8-bit breadboard computer](images/breadboard-computer.jpg)

*The completed 8-bit computer showing ~200 hand-wired connections, logic gates, LEDs, and 7-segment displays. The display shows "055" - output from a running Fibonacci sequence program.*

---

## Technical Specifications

### Hardware components

- **RAM:** 4-bit memory address (16 bytes total)
- **Registers:** Program Counter, A-register, B-register, Instruction register
- **ALU:** 8-bit addition and subtraction
- **Control unit:** 2 EEPROMs mapping instructions to control signals
- **Flags:** JMP, JZ (jump if zero), JC (jump if carry) for branching
- **Clock:** Bistable 555 timer (manual/automatic modes)
- **Output:** Three 7-segment displays + LEDs

### Programs it can run

- Multiplication via repeated addition (e.g., 6 × 8 = 48)
- Fibonacci sequence: 0,1,1,2,3,5,8,13,21,34,55,89,144,233
- Counting loops (0→255, 255→0)
- Conditional branching tests
