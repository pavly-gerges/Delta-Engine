# A physical abstraction for robotics: Delta-Engine

## Abstract
Scientific abstractions are one of the very useful techniques to implement software to control embedded microcontrollers for heavy machinery operations. In this paper, we introduce a physics engine that provides a new software paradigm for IO control for embedded systems and robotics based on a mathematical-physical abstraction.

## Keywords
Embedded Systems - Embedded IO - C Programming Framework - Calculus-based Physics - Multivariate Calculus - Software programming paradigms - System Entity Structure/Model Base (SES/MB) - Hardware Abstraction Layer (HAL) - Entity Component System (ECS) - Automata Theory

## Knowledge Gaps (Statement of Need)
There are a couple of theoretical and practical knowledge gaps that this software is going to address including, but not limited to:
- [ ] Precisional IO Embedded Control of heavy machines and robotics using Scientific Abstractions (e.g., Mathematical/Physical and Chemical Abstractions).
- [ ] Seamless hardware implementation of several physics simulation systems.
- [ ] Single abstraction for software and hardware systems.

## Introduction
Delta-Engine is a physics engine that provides a new software architectural paradigm for precisional IO switch and control over embedded systems and robotics without much knowledge in embedded systems, managing states and software engineering paradigms or if they fail to design the system (e.g., Object-oriented programming). It introduces the field of computational physics to the embedded world through providing a virtual machine and a runtime infrastructure based on the Newtonian physics spaces and supporting infrastructure IO libraries for several supported platforms.

## Methodologies
- Virtualization of physics objects and IO emulation using mathematical and physical abstractions.
- Newtonian physics spaces as Runtime Infrastructure (RTI).
- The Abstract architectural design methodologies involve using the **Hardware-Abstraction Layer (HAL)** to model the structure of the engine in a hierarchial form and the **System-Entity-Structure/Model-Base (SES/MB) Framework** to model the structure of the engine in a more detailed form and model the relation among the subsystems and the components of the engine.
- The Detailed-design methodologies involve using **Entity-Component-System (ECS)** to implement the structure of the physics engine together with the **Automata Theory**; such that, each component of the physics architecture could be represented by a system of component objects, and the system part of the ECS encapsulates state-machines; either deterministic or non-deterministic; with cyclic or non-cyclic runtime.
- Therefore, the theoretical methodology of the detailed-design is the **Entity-Component-Automata (ECA)**, a formal forge of the ECS and the Automata Theory.
- Implementation of several physics spaces modules (e.g., Kinematics Module - Fluid Mechanics Module); as systems of the ECA.
- Building preset physics components and automata that encapsulate the mathematical/physical abstraction.
- Formal linkage among the automata involved and the hardware drivers layer via callback functions $$\zeta$$; dispatched with each state transition via the transition functions $$\delta$$.

## High-level Architecture
<img src="https://electrostat-lab.github.io/Delta-Engine/architecture.svg" />

<img src="https://electrostat-lab.github.io/Delta-Engine/ses-mb.svg" />

Two architectural models are being proposed here; a **hierarchial model** representing a hardware abstraction layer using a mathematical/physical abstraction, and a **System-Entity-Structure/Model-Base (SES/MB) model** to model the same system components into several subsytems; those subsystems display some components that may be formally linked with components from other subsystems (e.g., the formal linkage among Math Libraries, Mechanics Libraries, and the VMIO Libraries that enable a chained dispatch from Physics to IO).

### Subsystems:
* Atomic Newtonian RTI: a subsystem that groups the runtime infrastructure components; its instantiation reveals the base Newtonian physics of inertia, acceleration, and object interaction in space.
    * Molecular Component.
    * Inertial Ref. frame Component.
    * Acceleration Component.
    * Interaction Component.
* Physics Mechanics: a specialized subsystem of the Newtonian RTI; grouping the different types of objects in the universe that experience inertia, acceleration/deceleration, and interaction with other objects.
    * Solid Mechanics Module.
    * Fluid Dynamics Module.
    * Thermodynamics Module.
    * Electromagnetism Module.
* Mathematical Libraries: a subsystem housing the base continous and discrete mathematical layer of the operations involved in the Physics Subsystems (both the Atomic/Newtonian RTI and the Physics Mechanics Subsystems).
    * Calculus Module.
    * VectorMath Module.
    * Matrix Algebra Module. 
* Virtualized IO (VMIO): a subsystem involving a platform-independent layer of driver modules to operate on the lower level platform-dependent IO infrastructure based on the output data from the Mathematical/Physical layers.
    * Analog Driver Module.
    * Digital Driver Module.
    * Comm Driver Module.
    * Memory Driver Module.
* IO Infrastructure: a subsystem involving a more platform specific dependent layer of the hardware IO; grouped together in a thin abstraction layer that encapsulates a procedural runtime for the hardware IO involved; links statically with **the Platform-dependent toolchain**.
    * GPIO Module.
    * PWM Module.
    * UART Module.
    * SPI Module.
    * I2C Module.
    * EEPROM Module. 
* Platform-dependent toolchain: a subsystem involving a platform-dependent layer of the hardware IO and the operating system operations that are encapsulated directly by the IO Infrastructure subsystem and indirectly by the Platform-agnostic VMIO subsystem.
    * Android Userspace Runtime.
    * AVR Runtime.
    * ARM Runtime.
    * x86 Userspace Runtime.

### Detailed Design:
Detailed design could be carried out using the **Entity-Component System (ECS) Framework** to model the structure of the engine, and the **Automata Theory** to model the behavior of the engine. Both could be linked via the system part of the ECS; ECS systems can be state machines with callback functions $$\zeta$$ dispatched after each state-state transition or from the $$\delta$$ transition function; either deterministic or non-deterministic; cyclic or non-cyclic in runtime behavior.
 
> [!NOTE]
> ## Example:
> A physics object; a ball; has the following:
> 1) A component that is attached to the **Inertial Ref. Frame System** through an entity `ID_BALL`.
> 2) A component that is attached to the **Acceleration/Deceleration System** through an entity `ID_BALL`.
> 3) A component that is attached to the **Molecular System** through an entity `ID_BALL`.
> 4) A component that is attached to the **Interaction System** through an entity `ID_BALL`.
> 5) A component that is attached to the **Mechanics System** through an entity `ID_BALL`.
> 
> ## Remarks:
> * It's not ideal to add a component of the ball object to the **Fluid Dynamics System**; therefore, both the **Solid Mechanics** and the **Fluid Dynamics** are specializations of the **Atomic/Newtonian RTI Subsystem**.
> * It would be ideal to attach a component of the ball object to the **Fluid Dynamics System**, only if the ball is highly deformable and could be expressed in terms of fluid or semi-fluid properties (e.g., the ball is a "thrombus" in biomedical simulation).
> * If that ball object is otherwise, a metallic object; it would be ideal to attach a component of it under the **Electromagnetism System**; as it could be electromagnetized under a magnetic field.
> * A ball object could have { **a standard mechanical component**, **a deformable component**, and **a magnetizable component** } at the same time to enable the different types of simulations accordingly under their respective systems { **Solid Mechanics System**, **Fluid Dynamics System**, and **Electromagnetism System**}, respectively.
> * The collection of the previous systems represent the core of the Delta-Engine; the **Atomic/Newtonian RTI Subsystem** and its specialization **Physics Mechanics**.
> * Systems are operated using State-Machines; either deterministic or non-deterministic in nature; cyclic or non-cyclic.
> * The methodology by which the Delta-Engine operates the hardware is via the axiomatic linkage among the layered subsystems of the software, and the pre-compiled platform-agnostic hardware drivers layer.
> * This axiomatic linkage, described in the former bullet, is performed via a callback $$\zeta$$ function through the machines' transition functions $$\delta$$.

## References
- [The Electrostatic-Sandbox SDK for distributed simulation systems](https://github.com/Electrostat-Lab/Electrostatic-Sandbox)
- [SES/MB Framework by Throsten Pawletta](https://dl.acm.org/doi/10.5555/3108244.3108245)
- [The Feynman Lectures Caltech University](https://www.feynmanlectures.caltech.edu/)
- [Physics for Scientists and Engineers, 6th Edition](https://www.amazon.com/Physics-Scientists-Engineers-Paul-Tipler/dp/142920124X)
- [Thomas' Calculus, 15th Edition](https://www.pearson.com/en-us/subject-catalog/p/thomas-calculus/P200000007103/9780137616077)
