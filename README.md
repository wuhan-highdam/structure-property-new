# structure-property
Particle based structural characterization.
本文件用于计算颗粒体系的结构序特征。

所需要的扩展包、版本。
pyvoro-mmalahe  1.3.3
pyboo           1.0.0
requests        2.23.0
openpyxl        3.0.3
pandas          1.0.1
numpy           1.18.1
numba           0.48.0
scipy           1.4.1
xlrd            1.2.0
matplotlib      3.2.0

输入：直接由LIGGGHTS输出的颗粒位置文件。(dump-   .sample)

输出：包含三个sheet的xlsx表格文件。
      sheet1：symmetry feature 72个特征；
      sheet2：interstice distribution 60个特征；
      sheet3：conventional feature 265个特征（MRO）或者 14个特征（SRO）；
      
文件主函数： main_function(path_, path_output_, scenario, MRO_option, Compute_feature_category)   
参数： 
path_: 颗粒位置文件路径
path_output_：文件输出路径
scenario：待处理的frame数
d50：待计算颗粒体系的d50
MRO_option：True 或者 False，判断是否计算输出传统结构序的MRO量。
MRO_option = True时：
sheet3包含：
1、Coordination number by Voronoi tessellation、Coordination number by cutoff distance (SRO and MRO).
Reference[1]: Okabe, A., Boots, B., Sugihara, K. & Chiu, S. N. Spatial Tesselations. Concepts and Applications                           of Voronoi Diagrams (John Wiley & Sons, 2009).

2、Voronoi idx3…7(SRO and MEO).
Reference[1]: Okabe, A., Boots, B., Sugihara, K. & Chiu, S. N. Spatial Tesselations. Concepts and Applications of                       Voronoi Diagrams (John Wiley & Sons, 2009).

3、Local volume fraction(SRO and MEO).
4、i-fold symm idx3...7(SRO and MRO).
Reference[2]: Peng, H. L., Li, M. Z. & Wang, W. H. Structural signature of plastic deformation in metallic glasses.                      Phys. Rev. Lett. 106, 135503 (2011).

5、weighted i-fold symm idx3…7(SRO and MRO).

6、Bond orientation order parameters(SRO and MRO).

7、Modified BOO(SRO and MRO).
Reference[3]:https://pyboo.readthedocs.io/en/latest/intro.html
Reference[4]:Xia, C. et al. The structural origin of the hard-sphere glass transition in granular packing. Nat.                         Commun.
Reference[5]: Clusters of polyhedra in spherical confinement. Proc. Natl. Acad. Sci. U. S. A.

8、Cluster packing efficiency(SRO and MRO).
Reference[6]: Yang, L. et al. Atomic-scale mechanisms of the glass-forming ability in metallic glasses. Phys.                           Rev. Lett. 109, 105502 (2012).
                  
MRO_option = False时：
sheet3包含：
1、Coordination number by Voronoi tessellation
2、Local volume fraction
3、Modified BOO
4、Cluster packing efficiency
5、Anisotropic coefficient of voronoi cell
                  
Compute_feature_category: ['symmetry_feature', 'interstice_distribution', 'conventional_feature'] 需要计算的特征类别，以上三种可选择使用。



特别说明：
1、文件可计算多分散颗粒体系，计算方法不确定为最优，可根据计算条件酌情更改（主要包括邻域颗粒的确定方法以及cutoff距离的选择）。
2、文件第一部分对多分散颗粒体系计算symmetry functions有待完善，之后继续更新。
