---
title: "ProfileGPU Options"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# ProfileGPUとは
GPUの負荷を調べるためのデバッグコマンド（コンソールコマンド）。
Stat GPUよりもより詳細な情報が見える。

Lyraの下記画面でProfileGPUした際の例。
![](https://storage.googleapis.com/zenn-user-upload/711f77106cd0-20250502.png)
:::details ProfileGPU結果のログ
```
Cmd: r.ProfileGPU.ThresholdPercent 0.05
r.ProfileGPU.ThresholdPercent = "0.05"
Cmd: profilegpu
Profiling the next GPU frame
LogRHI: Perf marker hierarchy, total GPU time 384.92ms, Threshold: 0.05% 
LogRHI:  2.3% 8.86ms   Frame 17781 2368 draws 46620 prims 58522 verts 515 dispatches
LogRHI:  0.0% 0.00ms   WorldTick 
LogRHI:  0.0% 0.00ms   WorldTick 
LogRHI:  0.0% 0.00ms   SendAllEndOfFrameUpdates 
LogRHI:  0.0% 0.00ms   SendAllEndOfFrameUpdates 
LogRHI:  0.0% 0.00ms   RayTracingGeometry 
LogRHI:  0.0% 0.00ms   UpdateLumenSceneBuffers 
LogRHI:  1.9% 7.42ms   FRDGBuilder::Execute 152 draws 26636 prims 23626 verts 513 dispatches
LogRHI:     0.0% 0.01ms   ClearGPUMessageBuffer 1 dispatch 1 groups
LogRHI:     0.0% 0.03ms   UpdateAllPrimitiveSceneInfos 1 dispatch
LogRHI:        0.0% 0.03ms   Shadow.Virtual.ProcessInvalidations 1 dispatch
LogRHI:           0.0% 0.03ms   InvalidateInstancePagesLoadBalancerCS (2 batches) 1 dispatch 2 groups
LogRHI:     0.0% 0.00ms   ShaderPrint::UploadParameters 1 dispatch 1 groups
LogRHI:     0.0% 0.05ms   UpdateDistanceFieldAtlas 1 draw 1 prims 0 verts 2 dispatches
LogRHI:        0.0% 0.00ms   ClearBuffer(DistanceFields.DistanceFieldAssetWantedNumMips Size=2048bytes) 1 draw 1 prims 0 verts 
LogRHI:        0.0% 0.00ms   ComputeWantedMips 1 dispatch 27 groups
LogRHI:        0.0% 0.00ms   GenerateStreamingRequests 1 dispatch 5 groups
LogRHI:        0.0% 0.00ms   DistanceFieldAssetReadback 
LogRHI:     1.9% 7.23ms   Scene 150 draws 26634 prims 23626 verts 508 dispatches
LogRHI:        0.0% 0.00ms   AccessModePass[Graphics] (Textures: 0, Buffers: 1) 
LogRHI:        0.0% 0.01ms   FXSystemPreRender 
LogRHI:           0.0% 0.00ms   GPUParticles_PreRender 
LogRHI:        0.0% 0.06ms   GPU KeyGen & Sort 23 dispatches
LogRHI:           0.0% 0.06ms   GPUSort_Batch0(LowPrecision) 23 dispatches
LogRHI:              0.0% 0.01ms   KeyGen_FNiagaraGpuComputeDispatch 3 dispatches
LogRHI:              0.0% 0.05ms   Sort(408) 20 dispatches
LogRHI:        0.0% 0.00ms   NiagaraUpdateDrawIndirectBuffers 1 dispatch 1 groups
LogRHI:        0.0% 0.03ms   GPUSceneUpdate 1 draw 1 prims 0 verts 5 dispatches
LogRHI:           0.0% 0.01ms   GPUScene.UploadDynamicPrimitiveShaderDataForView 3 dispatches
LogRHI:              0.0% 0.00ms   GPUScene::SetInstancePrimitiveIdCS 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   UpdateGPUScene NumPrimitiveDataUploads 1 1 dispatch
LogRHI:                 0.0% 0.00ms   ScatterUpload[0] (Resource: GPUScene.PrimitiveData, Offset: 0) 1 dispatch 1 groups
LogRHI:              0.0% 0.01ms   GPU Writer Delegates 1 dispatch
LogRHI:                 0.0% 0.01ms   Niagara.UpdateMeshParticleInstances (30 Instances) 1 dispatch 1 groups
LogRHI:           0.0% 0.01ms   BuildRenderingCommandsDeferred(Culling=On) 1 draw 1 prims 0 verts 2 dispatches
LogRHI:              0.0% 0.00ms   ClearBuffer(InstanceCulling.Compaction.BlockInstanceCounts Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   ClearIndirectArgInstanceCount 1 dispatch 1 groups
LogRHI:              0.0% 0.01ms   CullInstances(UnCulled). Bin 0 1 dispatch 5 groups
LogRHI:              0.0% 0.00ms   CullInstances(Generic). Bin 1 
LogRHI:              0.0% 0.00ms   Instance Compaction Phase 1 
LogRHI:              0.0% 0.00ms   Instance Compaction Phase 2 
LogRHI:        0.0% 0.00ms   CopyBuffer(Skinning.AnimTransforms Size=15456bytes) 1 draw 1 prims 0 verts 
LogRHI:        0.0% 0.00ms   AccessModePass[Graphics] (Textures: 1, Buffers: 1) 
LogRHI:        0.0% 0.01ms   ClearDepthStencil (SceneDepthZ) 1 draw 0 prims 0 verts 
LogRHI:        0.0% 0.00ms   PrePass DDM_AllOpaqueNoVelocity (Forced by Nanite) 1 draw 1764 prims 1778 verts 
LogRHI:           0.0% 0.00ms   DepthPassParallel 1 draw 1764 prims 1778 verts 
LogRHI:              0.0% 0.00ms   ParallelDraw (Index: 0, Num: 1) 1 draw 1764 prims 1778 verts 
LogRHI:           0.0% 0.00ms   EditorPrimitives 
LogRHI:        0.0% 0.01ms   RenderVelocities 4 draws 5594 prims 4084 verts 
LogRHI:           0.0% 0.00ms   ClearRenderTarget(SceneVelocity, slice 0, mip 0) 1848x792 ClearAction 1 draw 0 prims 0 verts 
LogRHI:           0.0% 0.01ms   VelocityParallel 3 draws 5594 prims 4084 verts 
LogRHI:              0.0% 0.01ms   ParallelDraw (Index: 0, Num: 1) 3 draws 5594 prims 4084 verts 
LogRHI:        0.0% 0.02ms   Nanite::VisBuffer 1 dispatch
LogRHI:           0.0% 0.02ms   Nanite::InitContext 1 dispatch
LogRHI:              0.0% 0.02ms   RasterClear 1 dispatch 175x99 groups
LogRHI:        0.1% 0.49ms   Nanite::VisBuffer 6 draws 6 prims 0 verts 80 dispatches
LogRHI:           0.1% 0.49ms   Nanite::DrawGeometry 6 draws 6 prims 0 verts 80 dispatches
LogRHI:              0.0% 0.00ms   ScatterUpload[0] (Resource: SceneCulling.Items, Offset: 0, GroupSize: 1) 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   ScatterUpload[0] (Resource: SceneCulling.ItemChunks, Offset: 0, GroupSize: 1) 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   InitArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   InitArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   ClearBuffer(Nanite.SplitWorkQueue.StateBuffer Size=12bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   ClearBuffer(Nanite.OccludedPatches.StateBuffer Size=12bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.1% 0.37ms   MainPass 2 draws 2 prims 0 verts 36 dispatches
LogRHI:                 0.0% 0.02ms   HierarchyCellCull 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InstanceHierarchyAppendUncullable 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InstanceHierarchySanitizeInstanceArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   InstanceCull - GroupWork 1 dispatch 1 groups
LogRHI:                 0.0% 0.05ms   NodeAndClusterCull 7 dispatches
LogRHI:                    0.0% 0.00ms   InitNodeCullArgs 1 dispatch 2 groups
LogRHI:                    0.0% 0.01ms   NodeCull_0 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   NodeCull_1 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   NodeCull_2 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   NodeCull_3 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InitClusterCullArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   ClusterCull 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   CalculateSafeRasterizerArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   RasterBinCount 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   RasterBinReserve 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   RasterBinScatter 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinFinalize 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   SW Rasterize (Tessellated) 
LogRHI:                 0.0% 0.06ms   HW Rasterize (Triangles) 9 dispatches
LogRHI:                 0.1% 0.20ms   SW Rasterize (Triangles) 9 dispatches
LogRHI:                 0.0% 0.00ms   ClearVisiblePatchesArgs 
LogRHI:                 0.0% 0.00ms   PatchSplit 
LogRHI:                 0.0% 0.00ms   InitVisiblePatchesArgs 
LogRHI:                 0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinCount 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   RasterBinReserve 
LogRHI:                 0.0% 0.00ms   RasterBinScatter 
LogRHI:                 0.0% 0.00ms   RasterBinFinalize 
LogRHI:                 0.0% 0.00ms   SW Rasterize (Patches) 
LogRHI:                 0.0% 0.00ms   InitClearQueueArgs 
LogRHI:                 0.0% 0.00ms   ClearSplitQueue 
LogRHI:              0.0% 0.03ms   BuildPreviousOccluderHZB 3 dispatches
LogRHI:                 0.0% 0.02ms   BuildHZB 3 dispatches
LogRHI:                    0.0% 0.02ms   ReduceHZB(mips=[0;3] Furthest) 1024x512 1 dispatch 128x64 groups
LogRHI:                    0.0% 0.00ms   ReduceHZB(mips=[4;7] Furthest) 64x32 1 dispatch 8x4 groups
LogRHI:                    0.0% 0.00ms   ReduceHZB(mips=[8;9] Furthest) 4x2 1 dispatch 1 groups
LogRHI:              0.0% 0.07ms   PostPass 2 draws 2 prims 0 verts 36 dispatches
LogRHI:                 0.0% 0.00ms   HierarchyCellCull 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InstanceHierarchySanitizeInstanceArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   InstanceCull 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InstanceCull - GroupWork 1 dispatch 1 groups
LogRHI:                 0.0% 0.02ms   NodeAndClusterCull 7 dispatches
LogRHI:                    0.0% 0.00ms   InitNodeCullArgs 1 dispatch 2 groups
LogRHI:                    0.0% 0.01ms   NodeCull_0 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   NodeCull_1 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   NodeCull_2 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   NodeCull_3 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InitClusterCullArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   ClusterCull 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   CalculateSafeRasterizerArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinCount 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   RasterBinReserve 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinScatter 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinFinalize 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   SW Rasterize (Tessellated) 
LogRHI:                 0.0% 0.00ms   HW Rasterize (Triangles) 9 dispatches
LogRHI:                 0.0% 0.00ms   SW Rasterize (Triangles) 9 dispatches
LogRHI:                 0.0% 0.00ms   ClearVisiblePatchesArgs 
LogRHI:                 0.0% 0.00ms   PatchSplit 
LogRHI:                 0.0% 0.00ms   InitVisiblePatchesArgs 
LogRHI:                 0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   RasterBinCount 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   RasterBinReserve 
LogRHI:                 0.0% 0.00ms   RasterBinScatter 
LogRHI:                 0.0% 0.00ms   RasterBinFinalize 
LogRHI:                 0.0% 0.00ms   SW Rasterize (Patches) 
LogRHI:                 0.0% 0.00ms   InitClearQueueArgs 
LogRHI:                 0.0% 0.00ms   ClearSplitQueue 
LogRHI:              0.0% 0.00ms   NaniteFeedbackStatus 1 dispatch 1 groups
LogRHI:        0.0% 0.09ms   NaniteBasePass 3 draws 2 prims 6 verts 
LogRHI:           0.0% 0.09ms   Nanite::EmitDepthTargets 3 draws 2 prims 6 verts 
LogRHI:              0.0% 0.00ms   ClearRenderTarget(Nanite.ShadingMask, slice 0, mip 0) 1848x792 ClearAction 1 draw 0 prims 0 verts 
LogRHI:              0.0% 0.08ms   Emit Scene Depth/Resolve/Velocity 1 draw 1 prims 3 verts 
LogRHI:              0.0% 0.02ms   Emit Scene Stencil 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.00ms   FVirtualShadowMapArray::UpdatePhysicalPageAddresses 1 dispatch 16 groups
LogRHI:        0.0% 0.01ms   HZB 6 draws 144 prims 96 verts 
LogRHI:           0.0% 0.01ms   BeginOcclusionTests 6 draws 144 prims 96 verts 
LogRHI:              0.0% 0.01ms   BeginOcclusionTests 6 draws 144 prims 96 verts 
LogRHI:                 0.0% 0.01ms   BeginOcclusionTests 6 draws 144 prims 96 verts 
LogRHI:                    0.0% 0.01ms   ViewOcclusionTests 0 6 draws 144 prims 96 verts 
LogRHI:                       0.0% 0.00ms   ShadowFrustumQueries 
LogRHI:                       0.0% 0.00ms   GroupedQueries 1 draw 84 prims 56 verts 
LogRHI:                       0.0% 0.01ms   IndividualQueries 5 draws 60 prims 40 verts 
LogRHI:        0.0% 0.02ms   HZB 5 dispatches
LogRHI:           0.0% 0.02ms   BuildHZB(ViewId=0) 5 dispatches
LogRHI:              0.0% 0.02ms   BuildHZB 5 dispatches
LogRHI:                 0.0% 0.01ms   ReduceHZB(mips=[0;3] Closest Furthest) 1024x512 1 dispatch 128x64 groups
LogRHI:                 0.0% 0.00ms   ReduceHZB(mips=[4;7] Furthest) 64x32 1 dispatch 8x4 groups
LogRHI:                 0.0% 0.00ms   ReduceHZB(mips=[4;7] Closest) 64x32 1 dispatch 8x4 groups
LogRHI:                 0.0% 0.00ms   ReduceHZB(mips=[8;9] Furthest) 4x2 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ReduceHZB(mips=[8;9] Closest) 4x2 1 dispatch 1 groups
LogRHI:        0.0% 0.03ms   SortLights 3 draws 3 prims 0 verts 2 dispatches
LogRHI:           0.0% 0.03ms   ComputeLightGrid 3 draws 3 prims 0 verts 2 dispatches
LogRHI:              0.0% 0.03ms   CullLights 22x13x32 NumLights 1 NumCaptures 3 3 draws 3 prims 0 verts 2 dispatches
LogRHI:                 0.0% 0.01ms   ClearBuffer(NextCulledLightLink Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(NextCulledLightData Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(NumCulledLightsGrid Size=193024bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.01ms   LightGridInject LinkedList SingleThread 1 dispatch 6x4x8 groups
LogRHI:                 0.0% 0.00ms   LightGridFeedbackStatus 1 dispatch 1 groups
LogRHI:        0.0% 0.00ms   LightFunctionAtlasGeneration 
LogRHI:           0.0% 0.00ms   LightFunctionAtlas Generation 
LogRHI:        0.0% 0.03ms   SkyAtmosphereLUTs 5 dispatches
LogRHI:           0.0% 0.00ms   TransmittanceLut 1 dispatch 32x8 groups
LogRHI:           0.0% 0.01ms   MultiScatteringLut 1 dispatch 4x4 groups
LogRHI:           0.0% 0.01ms   DistantSkyLightLut 1 dispatch 1 groups
LogRHI:           0.0% 0.01ms   SkyViewLut 1 dispatch 24x13 groups
LogRHI:           0.0% 0.00ms   CameraVolumeLut 1 dispatch 8x8x4 groups
LogRHI:        0.1% 0.37ms   CustomDepth 7 draws 5596 prims 4086 verts 34 dispatches
LogRHI:           0.0% 0.00ms   AccessModePass[Graphics] (Textures: 3, Buffers: 2) 
LogRHI:           0.0% 0.01ms   CustomDepth 3 draws 5592 prims 4083 verts 
LogRHI:           0.1% 0.36ms   Nanite CustomDepth 4 draws 4 prims 3 verts 34 dispatches
LogRHI:              0.0% 0.02ms   Nanite::InitContext 1 dispatch
LogRHI:                 0.0% 0.02ms   RasterClear 1 dispatch 175x99 groups
LogRHI:              0.1% 0.30ms   Nanite::DrawGeometry 3 draws 3 prims 0 verts 33 dispatches
LogRHI:                 0.0% 0.00ms   InitArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.SplitWorkQueue.StateBuffer Size=12bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.1% 0.29ms   NoOcclusionPass 2 draws 2 prims 0 verts 31 dispatches
LogRHI:                    0.0% 0.01ms   InstanceCull - Explicit List 1 dispatch 1 groups
LogRHI:                    0.0% 0.03ms   NodeAndClusterCull 7 dispatches
LogRHI:                       0.0% 0.00ms   InitNodeCullArgs 1 dispatch 2 groups
LogRHI:                       0.0% 0.01ms   NodeCull_0 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_1 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_2 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_3 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   InitClusterCullArgs 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   ClusterCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   CalculateSafeRasterizerArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   RasterBinCount 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   RasterBinScatter 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SW Rasterize (Tessellated) 
LogRHI:                    0.0% 0.01ms   HW Rasterize (Triangles) 8 dispatches
LogRHI:                    0.0% 0.19ms   SW Rasterize (Triangles) 8 dispatches
LogRHI:                    0.0% 0.00ms   ClearVisiblePatchesArgs 
LogRHI:                    0.0% 0.00ms   PatchSplit 
LogRHI:                    0.0% 0.00ms   InitVisiblePatchesArgs 
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinCount 
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 
LogRHI:                    0.0% 0.00ms   RasterBinScatter 
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 
LogRHI:                    0.0% 0.00ms   SW Rasterize (Patches) 
LogRHI:                    0.0% 0.00ms   InitClearQueueArgs 
LogRHI:                    0.0% 0.00ms   ClearSplitQueue 
LogRHI:                 0.0% 0.00ms   NaniteFeedbackStatus 1 dispatch 1 groups
LogRHI:              0.0% 0.03ms   Nanite::EmitCustomDepthStencilTargets 1 draw 1 prims 3 verts 
LogRHI:                 0.0% 0.03ms   Emit Custom Depth/Stencil 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.12ms   LumenSceneUpdate: 37 card captures 0.005M texels 11 draws 741 prims 2220 verts 35 dispatches
LogRHI:           0.0% 0.01ms   ResampleLightingHistoryToCardCaptureAtlasCS 1 dispatch 85 groups
LogRHI:           0.0% 0.01ms   ClearCardCapture 1 draw 74 prims 222 verts 
LogRHI:           0.0% 0.00ms   Nanite::InitContext 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   ClearTextureRects(Nanite.VisBuffer64 PF_R32G32_UINT 512x512 Mip=0) 1 draw 74 prims 222 verts 
LogRHI:           0.0% 0.08ms   Nanite::RasterizeLumenCards 1 draw 1 prims 0 verts 28 dispatches
LogRHI:              0.0% 0.08ms   Nanite::DrawGeometry 1 draw 1 prims 0 verts 28 dispatches
LogRHI:                 0.0% 0.00ms   InitArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.07ms   NoOcclusionPass 1 draw 1 prims 0 verts 26 dispatches
LogRHI:                    0.0% 0.01ms   InstanceCull - Explicit List 1 dispatch 1 groups
LogRHI:                    0.0% 0.02ms   NodeAndClusterCull 7 dispatches
LogRHI:                       0.0% 0.00ms   InitNodeCullArgs 1 dispatch 2 groups
LogRHI:                       0.0% 0.01ms   NodeCull_0 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_1 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   NodeCull_2 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   NodeCull_3 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   InitClusterCullArgs 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   ClusterCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   CalculateSafeRasterizerArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   RasterBinCount 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   RasterBinScatter 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   HW Rasterize (Triangles) 6 dispatches
LogRHI:                    0.0% 0.01ms   SW Rasterize (Triangles) 6 dispatches
LogRHI:                 0.0% 0.00ms   NaniteFeedbackStatus 1 dispatch 1 groups
LogRHI:           0.0% 0.02ms   Nanite::LumenMeshCapturePass 2 draws 148 prims 444 verts 6 dispatches
LogRHI:              0.0% 0.01ms   LumenShadeCS 6 dispatches
LogRHI:                 0.0% 0.01ms   6 materials 6 dispatches
LogRHI:              0.0% 0.00ms   Mark Stencil 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   Emit Depth 1 draw 74 prims 222 verts 
LogRHI:           0.0% 0.01ms   CopyCardsToSurfaceCache 6 draws 444 prims 1332 verts 
LogRHI:              0.0% 0.00ms   CopyToSurfaceCache Depth 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   CompressToSurfaceCache Albedo 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   CopyToSurfaceCache Opacity 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   CompressToSurfaceCache Normal 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   CompressToSurfaceCache Emissive 1 draw 74 prims 222 verts 
LogRHI:              0.0% 0.00ms   CopyCardCaptureLightingToAtlas 1 draw 74 prims 222 verts 
LogRHI:        0.0% 0.00ms   CopyBuffer(NaniteRayTracing.AuxiliaryDataBuffer Size=32bytes) 1 draw 1 prims 0 verts 
LogRHI:        0.0% 0.00ms   RayTracingDynamicGeometry 
LogRHI:           0.0% 0.00ms   RayTracingDynamicUpdate 
LogRHI:        0.1% 0.22ms   RayTracingScene 1 draw 1 prims 0 verts 2 dispatches
LogRHI:           0.0% 0.00ms   ClearBuffer(FRayTracingScene::OutputStatsBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:           0.0% 0.01ms   RayTracingBuildInstanceBuffer 2 dispatches
LogRHI:           0.0% 0.00ms   FRayTracingScene::StatsReadback 
LogRHI:           0.0% 0.00ms   RayTracingBuildScene 
LogRHI:           0.0% 0.00ms   RayTracingBuildScene 
LogRHI:           0.1% 0.21ms   Other Children
LogRHI:        0.0% 0.00ms   SetRayTracingBindings 
LogRHI:        0.0% 0.01ms   ClearBuffer(Lumen.FeedbackAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:        0.0% 0.00ms   ClearBuffer(Lumen.Feedback Size=46400bytes) 1 draw 1 prims 0 verts 
LogRHI:        0.2% 0.58ms   LumenSceneLighting 10 draws 10 prims 0 verts 28 dispatches
LogRHI:           0.0% 0.03ms   BuildCardUpdateContext 5 dispatches
LogRHI:              0.0% 0.00ms   ClearCardUpdateContext 1 dispatch 1 groups
LogRHI:              0.0% 0.02ms   BuildPageUpdatePriorityHistogram 1 dispatch 157 groups
LogRHI:              0.0% 0.00ms   Select max update bucket 1 dispatch 2 groups
LogRHI:              0.0% 0.00ms   Build cards update list 1 dispatch 157 groups
LogRHI:              0.0% 0.00ms   SetCardPageIndexIndirectArgs 1 dispatch 1 groups
LogRHI:           0.1% 0.20ms   DirectLighting 7 draws 7 prims 0 verts 15 dispatches
LogRHI:              0.0% 0.06ms   CullTiles 38 lights 5 draws 5 prims 0 verts 7 dispatches
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.CardTileAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   SpliceCardPagesIntoTiles 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InitializeCardTileIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   CalculateCardTileDepthRanges 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.DirectLighting.LightTileAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.DirectLighting.LightTileAllocatorPerLight Size=256bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.DirectLighting.LightTileAllocatorForPerCardTileDispatch Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.01ms   BuildLightTiles 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ComputeLightTileOffsetsPerLight 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InitializeLightTileIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.DirectLighting.CompactedLightTileAllocatorPerLight Size=256bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.01ms   CompactLightTiles 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   ClearBuffer(Lumen.DirectLighting.ShadowTraceAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.03ms   Light Attenuation ShadowMask 4 dispatches
LogRHI:                 0.0% 0.03ms   ShadowMaskFromLightAttenuationPass(UEDPIE_0_L_Expanse.DirLight) 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ShadowMaskFromLightAttenuationPass(LightType=3,BatchedNum=3) 3 dispatches
LogRHI:              0.0% 0.00ms   InitShadowTraceIndirectArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.07ms   Offscreen shadows 1 draw 1 prims 0 verts 1 dispatch
LogRHI:                 0.0% 0.00ms   FLumenDirectLightingHardwareRayTracingIndirectArgsCS 1 dispatch 1 groups
LogRHI:                 0.0% 0.07ms   LumenDirectLightingHardwareRayTracingRGS 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.02ms   Lights 1 dispatch
LogRHI:                 0.0% 0.02ms   Batched lights 1 dispatch 1 groups
LogRHI:              0.0% 0.01ms   CombineLighting CS 1 dispatch 1 groups
LogRHI:           0.1% 0.35ms   Radiosity 3 draws 3 prims 0 verts 8 dispatches
LogRHI:              0.0% 0.00ms   ClearBuffer(Lumen.CardTileAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   SpliceCardPagesIntoTiles 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   InitializeCardTileIndirectArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   ClearBuffer(Lumen.Radiosity.CardTileAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   BuildRadiosityTiles 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   IndirectArgs 1 dispatch 1 groups
LogRHI:              0.1% 0.25ms   HardwareRayTracingRGS 92160x1 4x4 probes at 4 spacing 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.03ms   SpatialFilterProbes 1 dispatch 1 groups
LogRHI:              0.0% 0.01ms   ConvertToSH 1 dispatch 1 groups
LogRHI:              0.0% 0.03ms   Integrate 1 dispatch 1 groups
LogRHI:              0.0% 0.01ms   CombineLighting CS 1 dispatch 1 groups
LogRHI:        0.0% 0.01ms   GBufferClear 1 draw 0 prims 0 verts 
LogRHI:        0.0% 0.05ms   SkyAtmosphereEditor 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.05ms   SkyAtmosphereEditor 1 draw 1 prims 3 verts 
LogRHI:        0.1% 0.38ms   BasePass 10 draws 8323 prims 6421 verts 50 dispatches
LogRHI:           0.0% 0.01ms   BasePassParallel 4 draws 7358 prims 5862 verts 
LogRHI:              0.0% 0.01ms   ParallelDraw (Index: 0, Num: 1) 4 draws 7358 prims 5862 verts 
LogRHI:           0.1% 0.36ms   NaniteBasePass 5 draws 5 prims 0 verts 50 dispatches
LogRHI:              0.1% 0.36ms   Nanite::BasePass 5 draws 5 prims 0 verts 50 dispatches
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.DummyMultiViewIndices Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.DummyMultiViewRectScaleOffsets Size=16bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.PackedViews Size=16bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.05ms   Nanite::ShadeBinning 2 draws 2 prims 0 verts 3 dispatches
LogRHI:                    0.0% 0.00ms   CopyBuffer(Nanite.ShadingBinMeta Size=1024bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.02ms   ShadingCount 1 dispatch 88x50 groups
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.ShadingBinAllocator Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.01ms   ShadingReserve 1 dispatch 1 groups
LogRHI:                    0.0% 0.03ms   ShadingScatter 1 dispatch 88x50 groups
LogRHI:                 0.1% 0.30ms   ShadeGBufferCS 47 dispatches
LogRHI:           0.0% 0.00ms   EditorPrimitives 
LogRHI:              0.0% 0.00ms   SDPG_World 
LogRHI:           0.0% 0.01ms   SkyPassParallel 1 draw 960 prims 559 verts 
LogRHI:              0.0% 0.01ms   ParallelDraw (Index: 0, Num: 1) 1 draw 960 prims 559 verts 
LogRHI:        0.0% 0.01ms   CopyStencilToLightingChannels 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.01ms   <unnamed pass> 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.09ms   ShadowDepths 2 draws 2 prims 0 verts 21 dispatches
LogRHI:           0.0% 0.09ms   FVirtualShadowMapArray::BuildPageAllocation 2 draws 2 prims 0 verts 21 dispatches
LogRHI:              0.0% 0.00ms   ScatterUpload[0] (Resource: Shadow.Virtual.ProjectionData, Offset: 0, GroupSize: 5) 1 dispatch 5 groups
LogRHI:              0.0% 0.00ms   ClearBuffer(Shadow.Virtual.StatsBuffer Size=352bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   ClearIndirectDispatchArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   ClearPageTable(Shadow.Virtual.PageRequestFlags Size=2097152bytes) 1 dispatch 64x17 groups
LogRHI:              0.0% 0.00ms   ClearBuffer(Shadow.Virtual.DirtyPageFlags Size=65536bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   InitPageRectBounds 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   MarkCoarsePages 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   PruneLightGrid(Min=0,Max=0) 1 dispatch 36 groups
LogRHI:              0.0% 0.02ms   GeneratePageFlagsFromPixels(GBuffer,NumShadowMaps=17,{88,50}) 1 dispatch 88x50 groups
LogRHI:              0.0% 0.00ms   ClearPageTable(Shadow.Virtual.PageTable Size=2097152bytes) 1 dispatch 64x17 groups
LogRHI:              0.0% 0.00ms   ClearPageTable(Shadow.Virtual.PageFlags Size=2097152bytes) 1 dispatch 64x17 groups
LogRHI:              0.0% 0.00ms   UpdatePhysicalPages 1 dispatch 16 groups
LogRHI:              0.0% 0.01ms   PackAvailablePages 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   AppendPhysicalPageList 1 dispatch 16 groups
LogRHI:              0.0% 0.00ms   AppendPhysicalPageList(Counts) 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   AllocateNewPageMappings 1 dispatch 64x17 groups
LogRHI:              0.0% 0.00ms   GenerateHierarchicalPageFlags 1 dispatch 16 groups
LogRHI:              0.0% 0.01ms   PropagateMappedMips 1 dispatch 64x17 groups
LogRHI:              0.0% 0.01ms   InitializePhysicalPages 2 dispatches
LogRHI:                 0.0% 0.00ms   SelectPagesToInitialize 1 dispatch 16 groups
LogRHI:                 0.0% 0.01ms   InitializePhysicalMemoryIndirect 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   Feedback Status 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   AppendPhysicalPageList 1 dispatch 16 groups
LogRHI:              0.0% 0.00ms   AppendPhysicalPageList(Counts) 1 dispatch 1 groups
LogRHI:        0.1% 0.36ms   ShadowDepths 18 draws 10 prims 0 verts 101 dispatches
LogRHI:           0.0% 0.01ms   GPUScene.UploadDynamicPrimitiveShaderDataForView 3 dispatches
LogRHI:              0.0% 0.00ms   GPUScene::SetInstancePrimitiveIdCS 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   UpdateGPUScene NumPrimitiveDataUploads 2 2 dispatches
LogRHI:                 0.0% 0.00ms   ScatterUpload[0] (Resource: GPUScene.PrimitiveData, Offset: 0) 1 dispatch 2 groups
LogRHI:                 0.0% 0.00ms   ScatterUpload[0] (Resource: GPUScene.InstanceSceneData, Offset: 0, GroupSize: 1) 1 dispatch 1 groups
LogRHI:           0.0% 0.03ms   BuildRenderingCommandsDeferred(Culling=On) 1 draw 1 prims 0 verts 5 dispatches
LogRHI:              0.0% 0.00ms   ClearBuffer(InstanceCulling.Compaction.BlockInstanceCounts Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   ClearIndirectArgInstanceCount 1 dispatch 1 groups
LogRHI:              0.0% 0.01ms   CullInstances(UnCulled). Bin 0 1 dispatch 3 groups
LogRHI:              0.0% 0.01ms   CullInstances(Generic). Bin 1 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   Instance Compaction Phase 1 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   Instance Compaction Phase 2 1 dispatch 1 groups
LogRHI:           0.1% 0.25ms   RenderVirtualShadowMaps(Nanite) 7 draws 7 prims 0 verts 84 dispatches
LogRHI:              0.1% 0.24ms   Nanite::DrawGeometry 7 draws 7 prims 0 verts 80 dispatches
LogRHI:                 0.0% 0.00ms   InitArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Shadow.Virtual.CompactedViewsAllocation Size=8bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.01ms   CompactViewsVSM 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   InitArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.SplitWorkQueue.StateBuffer Size=12bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Nanite.OccludedPatches.StateBuffer Size=12bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.15ms   MainPass 2 draws 2 prims 0 verts 36 dispatches
LogRHI:                    0.0% 0.01ms   HierarchyCellCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InstanceHierarchyAppendUncullable 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InstanceHierarchySanitizeInstanceArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   InstanceCull - GroupWork 1 dispatch 1 groups
LogRHI:                    0.0% 0.05ms   NodeAndClusterCull 7 dispatches
LogRHI:                       0.0% 0.00ms   InitNodeCullArgs 1 dispatch 2 groups
LogRHI:                       0.0% 0.01ms   NodeCull_0 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_1 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_2 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   NodeCull_3 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   InitClusterCullArgs 1 dispatch 1 groups
LogRHI:                       0.0% 0.01ms   ClusterCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   CalculateSafeRasterizerArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   RasterBinCount 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   RasterBinScatter 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SW Rasterize (Tessellated) 
LogRHI:                    0.0% 0.01ms   HW Rasterize (Triangles) 9 dispatches
LogRHI:                    0.0% 0.02ms   SW Rasterize (Triangles) 9 dispatches
LogRHI:                    0.0% 0.00ms   ClearVisiblePatchesArgs 
LogRHI:                    0.0% 0.00ms   PatchSplit 
LogRHI:                    0.0% 0.00ms   InitVisiblePatchesArgs 
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinCount 
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 
LogRHI:                    0.0% 0.00ms   RasterBinScatter 
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 
LogRHI:                    0.0% 0.00ms   SW Rasterize (Patches) 
LogRHI:                    0.0% 0.00ms   InitClearQueueArgs 
LogRHI:                    0.0% 0.00ms   ClearSplitQueue 
LogRHI:                 0.0% 0.01ms   BuildPreviousOccluderHZB(VSM) 4 dispatches
LogRHI:                    0.0% 0.00ms   ClearIndirectDispatchArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SelectPagesForHZB 1 dispatch 16 groups
LogRHI:                    0.0% 0.00ms   BuildHZBPerPage 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   BuildHZBPerPageTop 1 dispatch 1 groups
LogRHI:                 0.0% 0.06ms   PostPass 2 draws 2 prims 0 verts 36 dispatches
LogRHI:                    0.0% 0.00ms   HierarchyCellCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InstanceHierarchySanitizeInstanceArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InstanceCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InstanceCull - GroupWork 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   NodeAndClusterCull 7 dispatches
LogRHI:                       0.0% 0.00ms   InitNodeCullArgs 1 dispatch 2 groups
LogRHI:                       0.0% 0.00ms   NodeCull_0 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   NodeCull_1 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   NodeCull_2 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   NodeCull_3 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   InitClusterCullArgs 1 dispatch 1 groups
LogRHI:                       0.0% 0.00ms   ClusterCull 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   CalculateSafeRasterizerArgs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinCount 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinScatter 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SW Rasterize (Tessellated) 
LogRHI:                    0.0% 0.01ms   HW Rasterize (Triangles) 9 dispatches
LogRHI:                    0.0% 0.00ms   SW Rasterize (Triangles) 9 dispatches
LogRHI:                    0.0% 0.00ms   ClearVisiblePatchesArgs 
LogRHI:                    0.0% 0.00ms   PatchSplit 
LogRHI:                    0.0% 0.00ms   InitVisiblePatchesArgs 
LogRHI:                    0.0% 0.00ms   RasterBinInit 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   RasterBinCount 
LogRHI:                    0.0% 0.00ms   ClearBuffer(Nanite.RangeAllocatorBuffer Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   RasterBinReserve 
LogRHI:                    0.0% 0.00ms   RasterBinScatter 
LogRHI:                    0.0% 0.00ms   RasterBinFinalize 
LogRHI:                    0.0% 0.00ms   SW Rasterize (Patches) 
LogRHI:                    0.0% 0.00ms   InitClearQueueArgs 
LogRHI:                    0.0% 0.00ms   ClearSplitQueue 
LogRHI:                 0.0% 0.00ms   NaniteFeedbackStatus 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   ClearIndirectDispatchArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   SelectPagesForHZB 1 dispatch 16 groups
LogRHI:              0.0% 0.00ms   BuildHZBPerPage 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   BuildHZBPerPageTop 1 dispatch 1 groups
LogRHI:           0.0% 0.06ms   RenderVirtualShadowMaps(Non-Nanite) 10 draws 2 prims 0 verts 6 dispatches
LogRHI:              0.0% 0.06ms   Batched 10 draws 2 prims 0 verts 5 dispatches
LogRHI:                 0.0% 0.05ms   CullingPasses 2 draws 2 prims 0 verts 5 dispatches
LogRHI:                    0.0% 0.00ms   ClearBuffer(Shadow.Virtual.VisibleInstanceWriteOffset Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   ClearIndirectArgInstanceCount 1 dispatch 1 groups
LogRHI:                    0.0% 0.03ms   CullPerPageDrawCommands 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   ClearBuffer(InstanceCulling.OutputOffsetBufferOut Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.00ms   AllocateCommandInstanceOutputSpaceCs 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   InitIndirectArgs1D 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   OutputCommandInstanceListsCs 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   RasterPasses 8 draws 0 prims 0 verts 
LogRHI:              0.0% 0.00ms   UpdateAndClearDirtyFlags 1 dispatch 16 groups
LogRHI:           0.0% 0.01ms   FVirtualShadowMapArray::MergeStaticPhysicalPages 3 dispatches
LogRHI:              0.0% 0.00ms   ClearIndirectDispatchArgs 1 dispatch 1 groups
LogRHI:              0.0% 0.00ms   SelectPagesToMerge 1 dispatch 16 groups
LogRHI:              0.0% 0.00ms   MergeStaticPhysicalPagesIndirect 1 dispatch 1 groups
LogRHI:        0.0% 0.11ms   Nanite::Readback 1 dispatch
LogRHI:           0.0% 0.00ms   Readback 
LogRHI:           0.0% 0.01ms   ClearStreamingRequestCount 1 dispatch 1 groups
LogRHI:        0.0% 0.00ms   ClearStencil (SceneDepthZ) 1 draw 0 prims 0 verts 
LogRHI:        0.6% 2.15ms   RenderDeferredLighting 27 draws 2275 prims 2832 verts 84 dispatches
LogRHI:           0.5% 1.81ms   DiffuseIndirectAndAO 14 draws 1072 prims 1040 verts 75 dispatches
LogRHI:              0.3% 1.00ms   LumenScreenProbeGather 11 draws 1069 prims 1037 verts 58 dispatches
LogRHI:                 0.0% 0.01ms   UniformPlacement DownsampleFactor=16 1 dispatch 11x7 groups
LogRHI:                 0.0% 0.00ms   ClearTextureUint(Lumen.ScreenProbeGather.ScreenTileAdaptiveProbeHeader R32_UINT 116x50 Mip=0) 1 dispatch 15x7 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.ScreenProbeGather.NumAdaptiveScreenProbes Size=4bytes) 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.01ms   AdaptivePlacement DownsampleFactor=8 1 dispatch 22x13 groups
LogRHI:                 0.0% 0.01ms   AdaptivePlacement DownsampleFactor=4 1 dispatch 44x25 groups
LogRHI:                 0.0% 0.00ms   SetupAdaptiveProbeIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.03ms   ComputeBRDF_PDF 1 dispatch 1 groups
LogRHI:                 0.1% 0.26ms   UpdateRadianceCaches 9 draws 1067 prims 1037 verts 26 dispatches
LogRHI:                    0.0% 0.00ms   ClearProbeIndirectionCS 1 dispatch 48x12x12 groups
LogRHI:                    0.0% 0.00ms   ClearProbeIndirectionCS 1 dispatch 18x6x6 groups
LogRHI:                    0.0% 0.01ms   TranslucentSurfacesMarkPass 8 draws 1066 prims 1037 verts 
LogRHI:                    0.0% 0.01ms   MarkRadianceProbes(ScreenProbes) 88x75 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   MarkRadianceProbesUsedByTranslucencyVolume 1 dispatch 11x7x7 groups
LogRHI:                    0.0% 0.01ms   UpdateCacheForUsedProbes 1 dispatch 48x12x12 groups
LogRHI:                    0.0% 0.01ms   UpdateCacheForUsedProbes 1 dispatch 18x6x6 groups
LogRHI:                    0.0% 0.00ms   ClearRadianceCacheUpdateResources 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   ClearRadianceCacheUpdateResources 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   AllocateUsedProbes 1 dispatch 48x12x12 groups
LogRHI:                    0.0% 0.00ms   AllocateUsedProbes 1 dispatch 18x6x6 groups
LogRHI:                    0.0% 0.00ms   SelectMaxPriorityBucket 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SelectMaxPriorityBucket 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   AllocateProbeTraces 1 dispatch 48x12x12 groups
LogRHI:                    0.0% 0.00ms   AllocateProbeTraces 1 dispatch 18x6x6 groups
LogRHI:                    0.0% 0.00ms   SetupProbeIndirectArgsCS 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SetupProbeIndirectArgsCS 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   GenerateProbeTraceTiles 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   GenerateProbeTraceTiles 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SetupTraceFromProbesCS 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SetupTraceFromProbesCS 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   HardwareRayTracingIndirectArgs BatchSize:2 1 dispatch 1 groups
LogRHI:                    0.0% 0.13ms   HardwareRayTracingRGS default 1 draw 1 prims 0 verts 
LogRHI:                    0.0% 0.01ms   CompositeTracesIntoAtlas 1 dispatch 1 groups
LogRHI:                    0.0% 0.02ms   FilterProbeRadiance Res=32x32 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   FilterProbeRadiance Res=8x8 1 dispatch 1 groups
LogRHI:                    0.0% 0.01ms   FixupBordersAndGenerateMips 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   FixupBordersAndGenerateMips 1 dispatch 1 groups
LogRHI:                 0.0% 0.03ms   ComputeLightingPDF 1 dispatch 1 groups
LogRHI:                 0.0% 0.02ms   GenerateRays 8x8 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearTraces 8x8 1 dispatch 1 groups
LogRHI:                 0.0% 0.08ms   TraceScreen(Scene) 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.ScreenProbeGather.CompactedTraceTexelAllocator Size=8bytes) 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   CompactTraces WaveOps:1 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   SetupCompactedTracesIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   LumenScreenProbeGatherHardwareRayTracingIndirectArgsCS 1 dispatch 1 groups
LogRHI:                 0.0% 0.14ms   HardwareRayTracingRGS default 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearBuffer(Lumen.ScreenProbeGather.CompactedTraceTexelAllocator Size=8bytes) 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   CompactTraces WaveOps:1 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   SetupCompactedTracesIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.03ms   RadianceCacheInterpolate 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   CompositeTraces 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   CalculateMoving 1 dispatch 1 groups
LogRHI:                 0.0% 0.02ms   FilterRadianceWithGather 1 dispatch 1 groups
LogRHI:                 0.0% 0.02ms   FilterRadianceWithGather 1 dispatch 1 groups
LogRHI:                 0.0% 0.02ms   FilterRadianceWithGather 1 dispatch 1 groups
LogRHI:                 0.0% 0.03ms   ScreenProbeConvertToIrradiance Format:0 WaveOpWaveSize:32 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   FixupBorders 1 dispatch 1 groups
LogRHI:                 0.0% 0.06ms   ShortRangeAO_ScreenSpace(Rays=4) 1 dispatch 175x99 groups
LogRHI:                 0.0% 0.12ms   Integrate 5 dispatches
LogRHI:                    0.0% 0.01ms   TileClassificationMark 1 dispatch 175x99 groups
LogRHI:                    0.0% 0.01ms   TileClassificationBuildLists 1 dispatch 22x13 groups
LogRHI:                    0.0% 0.07ms   SimpleDiffuse 1 dispatch 1 groups
LogRHI:                    0.0% 0.03ms   SupportImportanceSampleBRDF 1 dispatch 1 groups
LogRHI:                    0.0% 0.00ms   SupportAll 1 dispatch 1 groups
LogRHI:                 0.0% 0.07ms   TemporalReprojection(1399x789) 1 dispatch 175x99 groups
LogRHI:              0.0% 0.18ms   TranslucencyVolumeLighting 1 draw 1 prims 0 verts 4 dispatches
LogRHI:                 0.0% 0.13ms   HardwareRayTracing (raygen) 3432x75 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.02ms   SpatialFilter 1 dispatch 17x10x26 groups
LogRHI:                 0.0% 0.01ms   SpatialFilter 1 dispatch 17x10x26 groups
LogRHI:                 0.0% 0.01ms   SpatialFilter 1 dispatch 17x10x26 groups
LogRHI:                 0.0% 0.01ms   Integrate 44x25x26 1 dispatch 11x7x7 groups
LogRHI:              0.2% 0.58ms   LumenReflections 1 draw 1 prims 0 verts 13 dispatches
LogRHI:                 0.0% 0.01ms   TileClassificationMark(1399x789) 1 dispatch 175x99 groups
LogRHI:                 0.0% 0.01ms   TileClassificationBuildLists 1 dispatch 22x13 groups
LogRHI:                 0.0% 0.00ms   TileClassificationBuildTracingLists 1 dispatch 11x7 groups
LogRHI:                 0.0% 0.02ms   GenerateRays MaxRoughnessToTrace:0.40 RadianceCache 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ClearTraces 1 dispatch 1 groups
LogRHI:                 0.0% 0.05ms   TraceScreen(Scene) 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   SetupCompactionIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.01ms   CompactTracesOrderedWaveOps 1024 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   ReflectionCompactRaysIndirectArgs 1 dispatch 1 groups
LogRHI:                 0.0% 0.18ms   ReflectionHardwareRayTracingRGS default 1 draw 1 prims 0 verts 
LogRHI:                 0.0% 0.00ms   ClearEmptyTiles 1 dispatch 1 groups
LogRHI:                 0.0% 0.14ms   ReflectionsResolve DonwsampleFactor:2 1 dispatch 1 groups
LogRHI:                 0.0% 0.09ms   TemporalAccumulation 1 dispatch 1 groups
LogRHI:                 0.0% 0.06ms   Spatial 1 dispatch 1 groups
LogRHI:              0.0% 0.05ms   DiffuseIndirectComposite(DiffuseIndirect=ScreenProbeGather) 1399x789 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.01ms   InitTranslucencyLightingVolumeTextures 1 dispatch
LogRHI:              0.0% 0.01ms   ClearTranslucencyLightingVolumeCompute 64 1 dispatch 16x16x16 groups
LogRHI:           0.1% 0.27ms   Lights 11 draws 947 prims 1280 verts 8 dispatches
LogRHI:              0.1% 0.27ms   DirectLighting 11 draws 947 prims 1280 verts 8 dispatches
LogRHI:                 0.0% 0.04ms   InjectTranslucencyLightingVolume 4 draws 512 prims 1024 verts 
LogRHI:                    0.0% 0.04ms   InjectTranslucencyLightingVolume(View=0) 4 draws 512 prims 1024 verts 
LogRHI:                       0.0% 0.01ms   InjectTranslucencyLightingVolumeBatch(VolumeCascade=0,Max=32) 1 draw 128 prims 256 verts 
LogRHI:                       0.0% 0.02ms   InjectTranslucencyLightingVolume(VolumeCascade=0,VirtualShadowMap) 1 draw 128 prims 256 verts 
LogRHI:                       0.0% 0.00ms   InjectTranslucencyLightingVolumeBatch(VolumeCascade=1,Max=32) 1 draw 128 prims 256 verts 
LogRHI:                       0.0% 0.01ms   InjectTranslucencyLightingVolume(VolumeCascade=1,VirtualShadowMap) 1 draw 128 prims 256 verts 
LogRHI:                 0.0% 0.00ms   BatchedLights 1 draw 432 prims 247 verts 
LogRHI:                    0.0% 0.00ms   Light::StandardDeferred: B_AbilitySpawner4 1 draw 432 prims 247 verts 
LogRHI:                 0.1% 0.23ms   UnbatchedLights 6 draws 3 prims 9 verts 8 dispatches
LogRHI:                    0.1% 0.23ms   UEDPIE_0_L_Expanse.DirLight 6 draws 3 prims 9 verts 8 dispatches
LogRHI:                       0.0% 0.00ms   ClearRenderTarget(ShadowMaskTexture, slice 0, mip 0) 1848x792 ClearAction 1 draw 0 prims 0 verts 
LogRHI:                       0.1% 0.20ms   ShadowProjectionOnOpaque 4 draws 2 prims 6 verts 8 dispatches
LogRHI:                          0.0% 0.03ms   DistanceFieldShadows 3 draws 1 prims 3 verts 7 dispatches
LogRHI:                             0.0% 0.03ms   BeginRayTracedDistanceFieldShadow 2 draws 0 prims 0 verts 7 dispatches
LogRHI:                                0.0% 0.02ms   CullDistanceFieldObjectsForLight MeshSDF 2 draws 0 prims 0 verts 6 dispatches
LogRHI:                                   0.0% 0.00ms   ClearBuffer(DistanceField.ObjectIndirectArguments Size=20bytes) 1 dispatch 256 groups
LogRHI:                                   0.0% 0.00ms   CullMeshSDFObjectsToFrustum 1 dispatch 27 groups
LogRHI:                                   0.0% 0.00ms   ClearBuffer(ShadowTileNumCulledObjects Size=16384bytes) 1 dispatch 64 groups
LogRHI:                                   0.0% 0.00ms   ScatterMeshSDFsToLightGrid 64x64 1 draw 0 prims 0 verts 
LogRHI:                                   0.0% 0.00ms   ClearBuffer(ShadowNextStartOffset Size=4bytes) 1 dispatch 1 groups
LogRHI:                                   0.0% 0.00ms   ComputeCulledObjectStartOffset 1 dispatch 8x8 groups
LogRHI:                                   0.0% 0.00ms   ClearBuffer(ShadowTileNumCulledObjects Size=16384bytes) 1 dispatch 64 groups
LogRHI:                                   0.0% 0.00ms   ScatterMeshSDFsToLightGrid 64x64 1 draw 0 prims 0 verts 
LogRHI:                                0.0% 0.01ms   DistanceFieldShadowing 704x400 1 dispatch 88x50 groups
LogRHI:                             0.0% 0.00ms   Upsample 1 draw 1 prims 3 verts 
LogRHI:                          0.0% 0.16ms   VirtualShadowMapProjection(Input:GBuffer) 1 dispatch 175x99 groups
LogRHI:                          0.0% 0.01ms   CompositeVirtualShadowMapMask 1 draw 1 prims 3 verts 
LogRHI:                       0.0% 0.03ms   Light::StandardDeferred: DirLight 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.05ms   FilterTranslucentVolume 64x64x64 Cascades:2 2 draws 256 prims 512 verts 
LogRHI:              0.0% 0.03ms   Cascade0 1 draw 128 prims 256 verts 
LogRHI:              0.0% 0.03ms   Cascade1 1 draw 128 prims 256 verts 
LogRHI:        0.0% 0.01ms   TemporalSuperResolution 1 dispatch
LogRHI:           0.0% 0.01ms   TSR MeasureFlickeringLuma 1399x789 1 dispatch 88x50 groups
LogRHI:        0.0% 0.01ms   SkyAtmosphere 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   <unnamed pass> 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.02ms   ExponentialHeightFog 1 draw 2 prims 4 verts 
LogRHI:           0.0% 0.02ms   Fog 1 draw 2 prims 4 verts 
LogRHI:        0.0% 0.00ms   PostRenderOpsFX 
LogRHI:           0.0% 0.00ms   SetSceneTexturesUniformBuffer 
LogRHI:           0.0% 0.00ms   FXSystemPostRenderOpaque 
LogRHI:              0.0% 0.00ms   GPUParticles_PostRenderOpaque 
LogRHI:           0.0% 0.00ms   AsyncGpuTraceHelper::PostRenderOpaque 
LogRHI:              0.0% 0.00ms   NiagaraUpdateCollisionGroupsMap 
LogRHI:           0.0% 0.00ms   Niagara::PostRenderFinish 
LogRHI:           0.0% 0.00ms   UnsetSceneTexturesUniformBuffer 
LogRHI:        0.0% 0.18ms   Translucency 22 draws 2147 prims 2084 verts 
LogRHI:           0.0% 0.17ms   RenderTranslucency 21 draws 2139 prims 2080 verts 
LogRHI:              0.0% 0.01ms   CopySceneColor 1 draw 1 prims 3 verts 
LogRHI:                 0.0% 0.01ms   <unnamed pass> 1 draw 1 prims 3 verts 
LogRHI:              0.0% 0.07ms   Translucency(BeforeDistortion Parallel) 1399x789 2 draws 2 prims 1 verts 
LogRHI:                 0.0% 0.07ms   ParallelDraw (Index: 0, Num: 1) 2 draws 2 prims 1 verts 
LogRHI:              0.0% 0.00ms   ClearRenderTarget(Translucency.AfterDOF.Color, slice 0, mip 0) 1848x792 ClearAction 1 draw 0 prims 0 verts 
LogRHI:              0.0% 0.05ms   Translucency(AfterDOF Parallel) 1399x789 9 draws 1072 prims 1040 verts 
LogRHI:                 0.0% 0.05ms   ParallelDraw (Index: 0, Num: 1) 9 draws 1072 prims 1040 verts 
LogRHI:              0.0% 0.00ms   ClearRenderTarget(Translucency.AfterDOF.Modulate, slice 0, mip 0) 1848x792 ClearAction 1 draw 0 prims 0 verts 
LogRHI:              0.0% 0.03ms   Translucency(AfterDOFModulate Parallel) 1399x789 7 draws 1064 prims 1036 verts 
LogRHI:                 0.0% 0.03ms   ParallelDraw (Index: 0, Num: 1) 7 draws 1064 prims 1036 verts 
LogRHI:           0.0% 0.01ms   RenderVelocities 1 draw 8 prims 4 verts 
LogRHI:              0.0% 0.01ms   VelocityParallel 1 draw 8 prims 4 verts 
LogRHI:                 0.0% 0.01ms   ParallelDraw (Index: 0, Num: 1) 1 draw 8 prims 4 verts 
LogRHI:        0.0% 0.00ms   VSM Log Stats And Status 1 dispatch 1 groups
LogRHI:        0.0% 0.00ms   VirtualTextureUpdate 
LogRHI:        0.4% 1.59ms   PostProcessing 4 draws 3 prims 6 verts 24 dispatches
LogRHI:           0.0% 0.01ms   ComposeTranslucencyToNewSceneColor 1 draw 1 prims 3 verts 
LogRHI:              0.0% 0.01ms   ComposeTranslucencyToNewSceneColor(AfterDOF ModulateOnly) 1399x789 -> 1399x789 1 draw 1 prims 3 verts 
LogRHI:           0.3% 1.27ms   TemporalSuperResolution(sg.AntiAliasingQuality=3) 1399x789 -> 1920x1083 7 dispatches
LogRHI:              0.0% 0.01ms   TSR ClearPrevTextures 1399x789 1 dispatch 88x50 groups
LogRHI:              0.0% 0.07ms   TSR DilateVelocity(#0 MotionBlurDirections=0 ReprojectionField OutputIsMoving) 1399x789 1 dispatch 175x99 groups
LogRHI:              0.0% 0.08ms   TSR DecimateHistory(#3 ReprojectMoire ReprojectResurrection) 1399x789 1 dispatch 175x99 groups
LogRHI:              0.1% 0.43ms   TSR RejectShading(#49 TileSize=26 PaddingCostMultiplier=1.5 WaveSize=32 VALU=32bit FlickeringFramePeriod=2.000000 Resurrection) 1399x789 1 dispatch 54x31 groups
LogRHI:              0.0% 0.01ms   TSR SpatialAntiAliasing(#2 Quality=2) 1399x789 1 dispatch 175x99 groups
LogRHI:              0.1% 0.57ms   TSR UpdateHistory(#3 Quality=Epic R11G11B10 ReprojectionField SupportLensDistortion) 3840x2166 1 dispatch 480x271 groups
LogRHI:              0.0% 0.09ms   TSR ResolveHistory(#0 WaveSize=32 OutputMip1) 1920x1083 1 dispatch 320x181 groups
LogRHI:           0.0% 0.07ms   MotionBlur 1 draw 1 prims 0 verts 8 dispatches
LogRHI:              0.0% 0.02ms   Velocity Flatten(CameraMotionBlurOn) 1399x789 1 dispatch 88x50 groups
LogRHI:              0.0% 0.01ms   VelocityTileGatherCS 88x50 1 dispatch 6x4 groups
LogRHI:              0.0% 0.00ms   ClearBuffer(MotionBlur.TileCounters Size=20bytes) 1 draw 1 prims 0 verts 
LogRHI:              0.0% 0.00ms   MotionBlur FilterTileClassify 120x68 1 dispatch 8x5 groups
LogRHI:              0.0% 0.00ms   MotionBlur SetupFilter 1 dispatch 1 groups
LogRHI:              0.0% 0.03ms   MotionBlur FullResFilter(BlurDirections=1 MaxSamples=16 OutputMip1) 1920x1083 4 dispatches
LogRHI:                 0.0% 0.03ms   MotionBlur Filter(GatherHalfRes) 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   MotionBlur Filter(GatherFullRes) 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   MotionBlur Filter(ScatterAsGatherOneVelocityHalfRes) 1 dispatch 1 groups
LogRHI:                 0.0% 0.00ms   MotionBlur Filter(ScatterAsGatherOneVelocityFullRes) 1 dispatch 1 groups
LogRHI:           0.0% 0.02ms   Histogram 3 dispatches
LogRHI:              0.0% 0.00ms   ClearTextureUint(Histogram.Scatter32 R32_UINT 128x1 Mip=0) 1 dispatch 16 groups
LogRHI:              0.0% 0.01ms   Histogram Atomic 960x542 (CS) 1 dispatch 542 groups
LogRHI:              0.0% 0.00ms   Histogram Convert 1 dispatch 1 groups
LogRHI:           0.0% 0.00ms   HistogramEyeAdaptation (CS) 1 dispatch 1 groups
LogRHI:           0.0% 0.00ms   CopyEyeAdaptationToTexture (CS) 1 dispatch 1 groups
LogRHI:           0.0% 0.00ms   EnqueueCopy(EyeAdaptationBuffer) 
LogRHI:           0.0% 0.13ms   Bloom 960x542 4 dispatches
LogRHI:              0.0% 0.01ms   FFTBloom FinalizeApplyConstants(ScatterDispersion=0.120000) 1 dispatch 1 groups
LogRHI:              0.0% 0.03ms   FFT: Two-For-One Forward Horizontal of size 1024 of buffer 960 x 542 1 dispatch 1x542 groups
LogRHI:              0.0% 0.06ms   FFT: Apply Forward Vertical Transform, Multiply Texture, and InverseTransform size 1024 of buffer 1026 x 542 1 dispatch 1x1026 groups
LogRHI:              0.0% 0.02ms   FFT: Two-For-One Inverse Horizontal of size 1024 of buffer 1026 x 542 1 dispatch 1x542 groups
LogRHI:           0.0% 0.04ms   Tonemap 1920x1083 (PS GammaOnly=0) 2 draws 1 prims 3 verts 
LogRHI:        0.0% 0.04ms   Submit Lumen surface cache feedback 3 draws 3 prims 0 verts 3 dispatches
LogRHI:           0.0% 0.00ms   ClearBuffer(Lumen.CompactedFeedback Size=8192bytes) 1 draw 1 prims 0 verts 
LogRHI:           0.0% 0.00ms   ClearBuffer(Lumen.HashTableKeys Size=8192bytes) 1 draw 1 prims 0 verts 
LogRHI:           0.0% 0.00ms   ClearBuffer(Lumen.HashTableElementCounts Size=8192bytes) 1 draw 1 prims 0 verts 
LogRHI:           0.0% 0.00ms   Hash table indirect arguments 1 dispatch 1 groups
LogRHI:           0.0% 0.00ms   Build feedback hash table 1 dispatch 1 groups
LogRHI:           0.0% 0.00ms   Compact feedback hash table 1 dispatch 32 groups
LogRHI:           0.0% 0.00ms   Readback 
LogRHI:        0.0% 0.00ms   ExtractUniformBuffer 
LogRHI:     0.0% 0.00ms   EnqueueCopy(GPUMessageManager.MessageBuffer) 
LogRHI:  0.3% 1.19ms   FRDGBuilder::Execute 2216 draws 19984 prims 34896 verts 
LogRHI:     0.2% 0.68ms   SlateUI Title = LyraStarterGame - Unreal Editor 114 draws 4290 prims 8256 verts 
LogRHI:        0.2% 0.68ms   ElementBatch 114 draws 4290 prims 8256 verts 
LogRHI:     0.1% 0.32ms   SlateUI Title = GPU Visualizer 2036 draws 15050 prims 25776 verts 
LogRHI:        0.1% 0.31ms   ElementBatch 2036 draws 15050 prims 25776 verts 
LogRHI:     0.0% 0.17ms   SlateUI Title = LyraStarterGame Preview [NetMode: Standalone 0]  (64-bit/PC D3D SM6) 66 draws 644 prims 864 verts 
LogRHI:        0.0% 0.10ms   ElementBatch 6 draws 136 prims 272 verts 
LogRHI:        0.0% 0.01ms   GaussianBlur 4 draws 4 prims 12 verts 
LogRHI:           0.0% 0.00ms   DownsampleUI 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Horizontal 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.01ms   Vertical 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Upsample 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.01ms   ElementBatch 17 draws 156 prims 172 verts 
LogRHI:        0.0% 0.01ms   GaussianBlur 4 draws 4 prims 12 verts 
LogRHI:           0.0% 0.00ms   DownsampleUI 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Horizontal 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Vertical 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Upsample 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.01ms   GaussianBlur 4 draws 4 prims 12 verts 
LogRHI:           0.0% 0.00ms   DownsampleUI 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Horizontal 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Vertical 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Upsample 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.01ms   ElementBatch 15 draws 168 prims 196 verts 
LogRHI:        0.0% 0.01ms   GaussianBlur 4 draws 4 prims 12 verts 
LogRHI:           0.0% 0.00ms   DownsampleUI 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Horizontal 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Vertical 1 draw 1 prims 3 verts 
LogRHI:           0.0% 0.00ms   Upsample 1 draw 1 prims 3 verts 
LogRHI:        0.0% 0.00ms   ElementBatch 12 draws 168 prims 176 verts 
LogRHI:  0.0% 0.01ms   FRDGBuilder::Execute 2 dispatches
LogRHI:     0.0% 0.00ms   UpdateAllPrimitiveSceneInfos 2 dispatches
LogRHI:        0.0% 0.00ms   ScatterUpload[0] (Resource: SceneCulling.Items, Offset: 0, GroupSize: 1) 1 dispatch 1 groups
LogRHI:        0.0% 0.00ms   ScatterUpload[0] (Resource: SceneCulling.ItemChunks, Offset: 0, GroupSize: 1) 1 dispatch 1 groups
LogRHI:     0.1% 0.24ms   Other Children
LogRHI: Total Nodes 722 Draws 2368
```
:::

# 使い方
`ProfileGPU`をデバッグコマンドで実行。
結果がログに表示される。Editorで実行した場合はGPU Visualizerでも表示される。

# オプション
## r.ProfileGPU.Sort
負荷が高い順にソート行う等のオプションが設定できる。
下記のようにすると実行時間によるソートが行われる。
```
r.ProfileGPU.Sort 1
```
## r.ProfileGPU.ThresholdPercent
出力する項目のしきい値の設定。
負荷が大きいものだけピックアップしたい際に使用。

## r.ShowMaterialDrawEvents
マテリアル単位での負荷を見たいときに使用。
全体の計測結果は上がってしまうので、詳細をプロファイルする際に使用。

# 参考リンク
[Unreal Engine \- プロファイリング＆最適化の始め方 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/ZJDQ1Z-UE_profiling_and_optimization)
[UE5の最新グラフィクスを使いこなすためのN個の勘所 \| EGC2024 \(Yutaro Sawada & Nori Shinoyama\) \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/5ENRE6-EGC2024_NGraphicsTips)
[Unreal InsightsとProfileGPUから見るLumenとNanite ＋ 5\.4までのアップデート \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/K3G48Y-UnrealInsightsProfileGPULumenNanite)
[Unreal Engine の GPUDump ビューア ツール \| Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/gpudump-viewer-tool-in-unreal-engine)