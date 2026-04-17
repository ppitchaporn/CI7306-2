# Challenge 2: Object Detection with Feature Point Matching

6710422016 Pitchaporn Nimdum

## Data source credit

- Self-recorded footage
- Intel IoT sample videos (intel-iot-devkit on GitHub, CC BY 4.0)
Repository: [https://github.com/intel-iot-devkit/sample-videos.git](https://github.com/intel-iot-devkit/sample-videos.git)

## Technique & Parameters

- **Preprocessing & Descriptors:** 
CLAHE for contrast normalization and dual_consensus (parallel SIFT and AKAZE) to optimize feature extraction across varying textures.
- **Matching & Geometry:** 
Filters correspondences using Lowe’s ratio test and fits a Perspective Homography via RANSAC, enforcing convexity checks and aspect ratio tolerance to reject invalid quads.
- **Temporal Stability:** 
Utilizes a QuadSmoothBuffer with Exponential Moving Average (EMA) or Moving Average to stabilize bounding box corners against frame-to-frame jitter.
- **Multi-Pose Logic:** 
Implements independent multi-template matching with IoU-NMS and recursive RANSAC to resolve detections for multi-instance or non-rigid.

---

## Results by category

### 01_success_easy

#### 1. output_black-cat-collar.mp4

[deliverables/01_success_easy/case_01/output_black-cat-collar.mp4](deliverables/01_success_easy/case_01/output_black-cat-collar.mp4)

   **Technique and parameters:**  ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.3; clahe_enabled true; max_frame_side 960; temporal_smooth_window 8; animal_nonrigid true; nms_iou_threshold 0.45.

   **Source:** Self-recorded
   **Objects target:** Black cat face
   **Object type:** Animal
   **Caption:** Close-up black cat looking up: green eyes, white whiskers, patterned collar with bell.

#### 2. output_french-bulldog-floor.mp4

[deliverables/01_success_easy/case_02/output_french-bulldog-floor.mp4](deliverables/01_success_easy/case_02/output_french-bulldog-floor.mp4)

   **Technique and parameters:** dual_consensus(SIFT+AKAZE); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.31; clahe_enabled true; max_frame_side 960; temporal_smooth_window 9; animal_nonrigid true.

   **Source:** Self-recorded
   **Objects target:** French bulldog sitting dark floor
   **Object type:** Animal
   **Caption:** French Bulldog slumped sitting, bat ears, white neck patch, indoor brown floor.

#### 3. output_navara-rear-night.mp4

[deliverables/01_success_easy/case_03/output_navara-rear-night.mp4](deliverables/01_success_easy/case_03/output_navara-rear-night.mp4)

   **Technique and parameters:**  detector SIFT; ratio 0.78; min_matches 15; ransac_reproj_threshold 12.0; min_inlier_ratio 0.32; clahe_enabled true; max_frame_side 960; temporal_smooth_window 10.

   **Source:** Self-recorded
   **Objects target:** Silver pickup truck
   **Object type:** scale_texture
   **Caption:** Rear view of a silver pickup truck recorded under low-light nighttime conditions.

#### 4. output_rose-bicolor.mp4

[deliverables/01_success_easy/case_04/output_rose-bicolor.mp4](deliverables/01_success_easy/case_04/output_rose-bicolor.mp4)

   **Technique and parameters:**  detector SIFT; ratio 0.75; min_matches 14; ransac_reproj_threshold 12.0; min_inlier_ratio 0.33; clahe_enabled true; max_frame_side 960; temporal_smooth_window 10.

   **Source:** Self-recorded
   **Objects target:** Pink-white rose bloom
   **Object type:** scale_texture
   **Caption:** Close-up of a mottled pink-white rose against blurred neutral pavement.

#### 5. output_snow-trail-hiker.mp4

[deliverables/01_success_easy/case_05/output_snow-trail-hiker.mp4](deliverables/01_success_easy/case_05/output_snow-trail-hiker.mp4)

   **Technique and parameters:** dual_consensus(SIFT+AKAZE); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.35; clahe_enabled true; max_frame_side 960; temporal_smooth_window 10; object_type human.

   **Source:** Self-recorded
   **Objects target:** Person
   **Object type:** human
   **Caption:** Full-length figure on snow: dark quilted jacket, orange pack, grey boots, trees behind.

---

### 02_success_difficult

#### 1. output_atv-forest-trail.mp4

[deliverables/02_success_difficult/case_01/output_atv-forest-trail.mp4](deliverables/02_success_difficult/case_01/output_atv-forest-trail.mp4)

   **Technique and parameters:** dual_consensus(SIFT+AKAZE); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.35; clahe_enabled true; max_frame_side 960; temporal_smooth_window 12.

   **Source:** Self-recorded
   **Objects target:** Rider and ATV
   **Object type:** human
   **Caption:** Rear view of a person in a yellow helmet driving a ATV on a wooded trail.

   **Why difficult:** Continuous viewpoint shifts alter the scale and geometry of the target, degrading descriptor matching. Furthermore, complex background clutter (foliage) and partial occlusions reduce the number of valid keypoints, weakening the support set required for stable RANSAC homography estimation.

#### 2. output_bolt-barcode-line.mp4

[deliverables/02_success_difficult/case_02/output_bolt-barcode-line.mp4](deliverables/02_success_difficult/case_02/output_bolt-barcode-line.mp4)

   **Technique and parameters:**  detector SIFT; ratio 0.72; min_matches 16; ransac_reproj_threshold 8.0; min_inlier_ratio 0.38; clahe_enabled true; process_scale 0.9375; max_frame_side 960.

   **Source:** Self-recorded
   **Objects target:** Bolt
   **Object type:** Repetitive pattern
   **Caption:** Threaded metal fastener and white barcode label on a moving conveyor.

   **Why difficult:** Repetitive barcode geometry generates ambiguous feature descriptors, causing a high rejection rate during Lowe's ratio test. Conveyor motion reduces keypoint gradient contrast, leaving frames with insufficient inliers to reliably compute the perspective homography matrix

#### 3. output_pork-belly-grill.mp4

[deliverables/02_success_difficult/case_03/output_pork-belly-grill.mp4](deliverables/02_success_difficult/case_03/output_pork-belly-grill.mp4)

   **Technique and parameters:**  detector SIFT; ratio 0.75; min_matches 14; ransac_reproj_threshold 12.0; min_inlier_ratio 0.33; clahe_enabled true; max_frame_side 960.

   **Source:** Self-recorded
   **Objects target:** Raw pork belly strip on circular grate
   **Object type:** scale_texture
   **Caption:** Long strip of layered pork belly on a round metal grill or drain grate.

   **Why difficult:** Glossy meat and grill specularities change appearance frame to frame; scale_texture scenes need strong inliers to hold a planar homography.

#### 4. output_small-dog-blep.mp4

[deliverables/02_success_difficult/case_04/output_small-dog-blep.mp4](deliverables/02_success_difficult/case_04/output_small-dog-blep.mp4)

   **Technique and parameters:** dual_consensus(SIFT+AKAZE); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.31; clahe_enabled true; animal_nonrigid true; max_frame_side 960; temporal_smooth_window 9.

   **Source:** Self-recorded
   **Objects target:** Small dog with bee cap
   **Object type:** Animal
   **Caption:** Frontal close-up of a small dog in a bee cap, showing out-of-plane head rotations.

   **Why difficult:** Non-rigid animal deformation and 3D head tilts violate the planar surface assumption required for 2D perspective homography.

#### 5. output_trail-runner-vest.mp4

[deliverables/02_success_difficult/case_05/output_trail-runner-vest.mp4](deliverables/02_success_difficult/case_05/output_trail-runner-vest.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.35; clahe_enabled true; max_frame_side 960; temporal_smooth_window 11.

   **Source:** Self-recorded
   **Objects target:** Runner
   **Object type:** human
   **Caption:** Trail runner wearing a hydration vest, moving quickly past foreground bushes.

   **Why difficult:** Fast subject motion combined with partial occlusion by foliage physically blocks keypoints, driving the active match count below the RANSAC min_inlier_ratio threshold.

---

### 03_failed_expected

#### 1. output_heart-pendant-chain.mp4

[deliverables/03_failed_expected/case_01/output_heart-pendant-chain.mp4](deliverables/03_failed_expected/case_01/output_heart-pendant-chain.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 11; ransac_reproj_threshold 12.0; min_inlier_ratio 0.3; clahe_enabled true; use_scaled_matching false; process_scale 1.0.

   **Source:** Self-recorded
   **Objects target:** Silver ball chain and heart pendant
   **Object type:** transparent_reflection
   **Caption:** Jewelry close-up: bead chain and small green heart charm on skin-toned background.

   **Why it fails:** Specular chain and skin reflections change highlights; transparent_reflection breaks stable SIFT/AKAZE correspondences most frames.

   **Improvement:**  Tighter crops on matte, non-specular links; stronger clahe / blur tuning; more templates under templates_augmented for glare states; relax min_inlier_ratio slightly only if false negatives dominate.

#### 2. output_oven-flame-arch.mp4

[deliverables/03_failed_expected/case_02/output_oven-flame-arch.mp4](deliverables/03_failed_expected/case_02/output_oven-flame-arch.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 12; ransac_reproj_threshold 15.0; min_inlier_ratio 0.28; clahe_enabled true; independent_multi_template_matching false; temporal_smooth_window 10.

   **Source:** Self-recorded
   **Objects target:** Vertical flame in pizza oven
   **Object type:** flame
   **Caption:** Bright, flickering flame under a dark arch with an orange glowing interior.

   **Why it fails:** Flames are highly dynamic, non-rigid, and lack persistent textures. This fundamentally violates the rigid, planar surface assumption required to compute a valid 2D perspective transform.

   **Improvement:**  Part-based templates_augmented with anchor on static oven mouth; higher ransac_reproj_threshold only with static anchors; temporal smoothing cannot help without any successful frames.

#### 3. output_airfryer-purple-food.mp4

[deliverables/03_failed_expected/case_03/output_airfryer-purple-food.mp4](deliverables/03_failed_expected/case_03/output_airfryer-purple-food.mp4)

   **Technique and parameters:**  detector SIFT; ratio 0.75; min_matches 14; ransac_reproj_threshold 12.0; min_inlier_ratio 0.34; clahe_enabled true; max_frame_side 960.

   **Source:** Self-recorded
   **Objects target:** Silver Fork
   **Object type:** scale_texture
   **Caption:** Silver fork piercing textured food on a white plate inside a dark air fryer.

   **Why it fails:** The uniform texture of the silver fork yields few distinct keypoints, causing the algorithm to inappropriately anchor to the highly textured food background. This leads to high template diversity rather than a simple low detection rate.

   **Improvement:** Crop templates strictly to the fork's structural boundaries to exclude the food texture. Consolidate to a single pose to enforce consistency.

---

#### 4. output_bike-white-pavement.mp4

[deliverables/03_failed_expected/case_04/output_bike-white-pavement.mp4](deliverables/03_failed_expected/case_04/output_bike-white-pavement.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.35; clahe_enabled true; use_scaled_matching false; nms_iou_threshold 0.42.

   **Source:** [https://github.com/intel-iot-devkit/sample-videos/blob/master/person-bicycle-car-detection.mp4](https://github.com/intel-iot-devkit/sample-videos/blob/master/person-bicycle-car-detection.mp4)

   **Objects target:** Person, bicycle, car
   **Object type:** human
   **Caption:** High-angle view of a car, human, and white bicycle against light grey pavement.

   **Why it fails:** Low pixel intensity variance between the white bike and grey pavement impedes edge gradient extraction, severely limiting scale-space extrema detection (DoG). System attempts to compensate by aggressively cycling through templates, yielding poor temporal continuity.

   **Improvement:** Tighten templates to a single dominant pose to eliminate false tier drift. Optimize CLAHE parameters to force stronger local contrast before descriptor extraction.

#### 5. output_produce-conveyor-blur.mp4

[deliverables/03_failed_expected/case_05/output_produce-conveyor-blur.mp4](deliverables/03_failed_expected/case_05/output_produce-conveyor-blur.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 20; ransac_reproj_threshold 12.0; min_inlier_ratio 0.4; clahe_enabled true; use_scaled_matching false; max_frame_side 960.

   **Source:** [https://github.com/intel-iot-devkit/sample-videos/blob/master/fruit-and-vegetable-detection.mp4](https://github.com/intel-iot-devkit/sample-videos/blob/master/fruit-and-vegetable-detection.mp4)
   **Objects target:** Fruit and vegetable
   **Object type:** multi_instance
   **Caption:** Assorted fruits and vegetables moving rapidly along a conveyor belt.

   **Why it fails:** Severe motion blur degrades spatial frequency, smoothing out the gradients necessary for SIFT keypoint localization. 

   **Improvement:** Lower the min_matches requirement to accommodate blurred frames, and decrease process_scale to artificially merge pixel noise into stronger low-frequency gradients.

### 04_failed_unexpected

#### 1. output_bicycle-wheel-crop.mp4

[deliverables/04_failed_unexpected/case_01/output_bicycle-wheel-crop.mp4](deliverables/04_failed_unexpected/case_01/output_bicycle-wheel-crop.mp4)

   **Technique and parameters:**  detector SIFT; ratio 0.76; min_matches 15; ransac_reproj_threshold 12.0; min_inlier_ratio 0.33; clahe_enabled true; max_frame_side 960.

   **Source:** Self-recorded
   **Objects target:** Yellow bicycle
   **Object type:** scale_texture
   **Caption:** People riding bicycles on a paved road adjacent to foliage.

   **Why it fails:** While frames contain high clarity (Laplacian variance), the repeating radial geometry of the bicycle spokes creates descriptor redundancy. This mathematical ambiguity inherently fails the Lowe ratio test.

   **Improvement:**  Crop to less motion-blurred spokes; add a template on a distinct tread or label patch; enable scaled matching if full-res noise dominates.

#### 2. output_classroom-desk.mp4

[deliverables/04_failed_unexpected/case_02/output_classroom-desk.mp4](deliverables/04_failed_unexpected/case_02/output_classroom-desk.mp4)

   **Technique and parameters:** dual_consensus(SIFT+AKAZE); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.35; clahe_enabled true; max_frame_side 960.

   **Source:** [https://github.com/intel-iot-devkit/sample-videos/blob/master/classroom.mp4](https://github.com/intel-iot-devkit/sample-videos/blob/master/classroom.mp4)
   **Objects target:** Seated/Standup person
   **Object type:** human
   **Caption:** Four young men dressed in similar tones behind a white table, with chest areas occluded.

   **Why it fails:**  Multiple subjects wearing identically colored clothing create cross-instance feature matching. RANSAC mistakenly combines inliers from different people into a single model, causing severe bounding box instability and jumping.

   **Improvement:** Allow recursive RANSAC for multiple instances.

#### 3. output_water-bottle-cap.mp4

[deliverables/04_failed_unexpected/case_03/output_water-bottle-cap.mp4](deliverables/04_failed_unexpected/case_03/output_water-bottle-cap.mp4)

   **Technique and parameters:** dual_consensus(SIFT+AKAZE); ratio 0.82; min_matches 20; ransac_reproj_threshold 12.0; min_inlier_ratio 0.4; clahe_enabled true; use_scaled_matching false; max_frame_side 960.

   **Source:** [https://github.com/intel-iot-devkit/sample-videos/blob/master/bottle-detection.mp4](https://github.com/intel-iot-devkit/sample-videos/blob/master/bottle-detection.mp4)
   **Objects target:** 3 clear plastic bottles with blue screw caps
   **Object type:** multi_instance
   **Caption:** Three clear water bottles with dark blue caps being picked up and moved interactively.

   **Why it fails:** Identical objects cause spatial ambiguity, but more critically, clear plastic generates dynamic specular reflections. As bottles move, shifting reflections severely alter local pixel gradients, breaking SIFT descriptor consistency.

   **Improvement:** Shift the template focus exclusively to the opaque, non-reflective blue caps. Apply draw_best_instance_only: false to enable tracking of all three independent caps simultaneously.

#### 4. output_pancake-griddle.mp4

[deliverables/04_failed_unexpected/case_04/output_pancake-griddle.mp4](deliverables/04_failed_unexpected/case_04/output_pancake-griddle.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 12; ransac_reproj_threshold 12.0; min_inlier_ratio 0.3; clahe_enabled true; preprocess_gaussian_sigma 1.0; max_frame_side 960.

   **Source:** Self-recorded
   **Objects target:** Pancake
   **Object type:** transparent_reflection
   **Caption:** Close-up of a golden-brown pancake cooking on a flat black cooking surface.

   **Why it fails:** Low detection_rate with occasional sharp frames (transparent_reflection on oil sheen) pushes the heuristic toward unexpected failure vs. purely low-clarity expected fail.

   **Improvement:**  Mask glare in templates; add templates for dry vs. glossy griddle; slightly lower min_matches for this stem via stem_overrides.

#### 5. output_site-hard-hat.mp4

[deliverables/04_failed_unexpected/case_05/output_site-hard-hat.mp4](deliverables/04_failed_unexpected/case_05/output_site-hard-hat.mp4)

   **Technique and parameters:** dual_consensus(SIFT+SIFT); ratio 0.82; min_matches 14; ransac_reproj_threshold 12.0; min_inlier_ratio 0.34; clahe_enabled true; max_frame_side 960.

   **Source:** [https://github.com/intel-iot-devkit/sample-videos/blob/master/worker-zone-detection.mp4](https://github.com/intel-iot-devkit/sample-videos/blob/master/worker-zone-detection.mp4)
   **Objects target:** Worker
   **Object type:** human
   **Caption:** Multiple workers wearing glossy yellow safety helmets walking back and forth.

   **Why it fails:** The glossy surface of the safety helmets creates specular highlights that shift independently of the object's physical movement. This distorts the underlying gradient orientations, causing valid feature points to fail descriptor matching.

   **Improvement:** Preprocess frames with stricter CLAHE parameters to suppress intense specular lighting , or capture templates prioritizing matte surfaces rather than the highly reflective helmets.