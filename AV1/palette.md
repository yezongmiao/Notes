# 记录代码流程

    av1_rd_pick_palette_intra_sby（）
有效的输入参数为：

    const AV1_COMP *const cpi 
    MACROBLOCK *x

    MB_MODE_INFO *best_mbmi
    uint8_t *best_palette_color_map
    int64_t *best_rd

临时变量：
根据编码bit位设定buffer，高bit位用4096，低bit位用256，用于存放颜色的直方图情况。

    int count_buf[1 << 12];    //4096
    int count_buf_8bit[1 << 8];   //256

根据已知的块推断当前块的Palette的颜色cache,并且记录载入的颜色数量。

    uint16_t color_cache[2 * PALETTE_MAX_SIZE];
    const int ncache

下面变量是输出颜色的种类情况。

    int colors, colors_threshold

Palette：

    centroids[PALETTE_MAX_SIZE]

一个块中，前面几种的颜色情况：

    int top_colors[PALETTE_MAX_SIZE]

提前中断搜索的信号，传入rdcost计算函数中，初始化是False：

    do_header_rd_based_breakout
