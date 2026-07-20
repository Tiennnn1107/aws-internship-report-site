---
title: "Event 23/5/2026 - FCAJ Community Day"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# FCAJ Community Day Reflection

On 23 May 2026, I attended FCAJ Community Day with a friend. The event covered several topics, including working with AI context, Amazon Quick, CloudFront, hackathon experience, LLM non-determinism, and enterprise Multi-Agent systems. This reflection focuses on the ideas that were most relevant to my own learning and project.

## Sessions

- Tịnh: **Context Is Everything**.
- Phạm Ngô Hải Anh: **Friendly AI Assistant with Amazon Quick**.
- Nguyễn Tuấn Thịnh: **From Edge to Origin**.
- Team VIB: **36 Hours with LotusHacks**.
- Đào Đức: **Non-Determinism of Deterministic LLM Settings**.
- Cát Vy: **Enterprise-Grade Multi-Agent System**.

## My Main Takeaways

### Useful context is better than excessive context

I previously assumed that a longer prompt would usually produce a better answer. The session helped me understand that relevance matters more than length. Good context should define the goal, necessary data, constraints, and expected output. Adding unrelated documents can hide important details and increase token use.

The “Second AI Brain” idea was also interesting. A system can store documents, retrieve only the relevant information, and then provide it to the model. This approach could be useful for managing study notes or long-term project documentation.

### AI assistants need data controls

The Amazon Quick session demonstrated how an enterprise assistant can connect to different data sources and support research, reporting, and repetitive tasks. One example was a Project Manager assistant that could prepare meeting notes, send emails, and schedule the next meeting.

I learned that convenience must be balanced with access control. An assistant working with internal company data must only retrieve information that the current user is authorized to see.

### CloudFront provides more than caching

The CloudFront session was especially relevant to my RecruitPro project. CloudFront can reduce requests to the origin, serve content closer to users, support HTTPS, and work with AWS Shield and AWS WAF. It therefore contributes to performance, availability, cost control, and security.

This clarified why an application should avoid exposing its origin directly whenever possible.

### A focused hackathon product is easier to finish

Team VIB described building UTMorpho during the 36-hour LotusHacks competition. The team faced limited time and tokens, fatigue, coordination difficulties, and AI-generated content that was not always useful. Their progress improved after they focused on the main editing experience instead of adding too many ideas.

My takeaway was that one stable and demonstrable feature is more valuable than many incomplete features when time is limited.

### Temperature zero is not a complete guarantee

I was surprised that the same prompt can still produce slightly different results even when temperature is set to zero. GPU calculations, parallel processing, and request batching can contribute to these differences.

Important AI features should therefore validate model output instead of assuming that it is fixed. Structured output, JSON formats, constrained responses, and repeated tests can make integration more reliable.

### Enterprise Multi-Agent systems require control

The final session used startup credit assessment as a Multi-Agent example. Specialized agents analyzed finance, market conditions, the founding team, risk, and compliance, while a manager agent coordinated the process.

Specialization can improve parallel work and cross-checking, but an enterprise system also needs access limits, data protection, audit records, output validation, and human review. This is an important difference between an AI demo and a production system.

## Lessons I Can Apply

- Provide relevant context instead of sending all available information to AI.
- State goals, constraints, and output formats clearly.
- Use CloudFront to protect and reduce traffic to the origin, not only to cache content.
- Prioritize the core feature when building under a short deadline.
- Do not treat temperature zero as a guarantee of identical output.
- Validate input, output, and tool permissions in AI Agent systems.

## Connection to My Project

The CloudFront topic is the first lesson I can apply to RecruitPro. I can review cache behaviors, limit direct origin access, and learn how AWS WAF could be added. For AI tasks, I will write more structured prompts and review generated results before using them.

## Proof of Attendance

![My photo at FCAJ Community Day](</images/4-EventParticipated/4.1-Event1/check-in-fcaj-community-day.jpg>)

![Photo taken during the event](</images/4-EventParticipated/4.1-Event1/chia-se-cloudfront-bao-ve-ddos.jpg>)

## Conclusion

FCAJ Community Day gave me practical perspectives on both AWS and AI. CloudFront was the most directly relevant session for my current project, while the LLM and Multi-Agent topics showed me that real AI applications need more validation and control than simple demonstrations. These are areas I would like to continue exploring in future projects.
