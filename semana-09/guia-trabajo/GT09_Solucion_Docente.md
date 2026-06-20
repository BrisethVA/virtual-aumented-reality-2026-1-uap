# GT09 — SOLUCIÓN DOCENTE
## ⚠️ CONFIDENCIAL

## PARTE I: b, b, b, b, c, b

## PARTE II
1. draw calls
2. Static
3. baking (o "lightmap baking" / "Generate Lighting")
4. idénticos
5. iluminación
6. extrude (extrusión)

## PARTE III

**3.1:**
| Valor | Problema | Impacto |
|-------|---------|---------|
| 347 Draw Calls | Excede límite móvil (≤100). Materiales sin batching | GPU sobrecargado → bajo FPS |
| 2.1M Tris | Demasiada geometría para dispositivo móvil | Vértices saturan pipeline gráfico |
| 12 FPS | No apto para AR/VR (mínimo 30 para AR, 60 para VR) | Experiencia inutilizable, posible mareo |

**3.2:**
| Técnica | Cómo | Mejora |
|---------|------|--------|
| Static Batching | Marcar objetos estáticos como Static, asegurarse que compartan materiales | Draw Calls de 347 a ~50-80 |
| LOD Groups | Para objetos lejanos usar modelo con menos triángulos | Tris de 2.1M a ~200-400K |
| Baked Lighting | Configurar luces como Baked, Generate Lighting | Eliminación del cálculo de sombras en runtime |

## PARTE IV: Aceptar cualquier diseño coherente con el proyecto del grupo.

*PSISP08075 | CONFIDENCIAL | 2026-1*
