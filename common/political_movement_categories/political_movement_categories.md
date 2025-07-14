movement_pop_support_example = { -- 运动人口支持示例 (类别)
    # 该类运动的 2D 图标
    icon = "gfx/interface/icons/political_movement_icons/movement_religious.dds" -- 图标 = ...

    # 如果为 yes，该类运动在创建时总会带有明确的文化身份
    cultural_identity = yes/no -- 文化身份 = 是/否

    # 如果为 yes，该类运动在创建时总会带有明确的宗教身份
    religious_identity = yes/no -- 宗教身份 = 是/否

    # 如果为 yes，最低支持值将仅查看该运动特定文化/宗教身份内部的支持度
    # 除非启用了 cultural_identity 或 religious_identity，否则无效
    minimum_support_is_within_identity = yes/no -- 最低支持是否在身份内 = 是/否

    # 创建该类运动所需的最低预测支持值
    minimum_support_to_create = x -- 创建所需最低支持 = x

    # 该类运动不解散所需的最低预测支持值
    # 新创建的运动在检查此值之前有一段定义的宽限期
    minimum_support_to_maintain = x -- 维持所需最低支持 = x
}