movement_example = { -- 运动示例
    # 运动的类别，决定了它是否具有文化/宗教身份等因素
    # 运动类别在它们自己的数据库中定义
    category = x -- 类别 = x

    # 运动的核心意识形态 - 这将决定他们固有地支持/反对哪些法律
    ideology = x -- 意识形态 = x

    # 该运动可能分配给其施压的利益集团（IG）领导者的角色意识形态列表
    character_ideologies = {} -- 角色意识形态 = {}

    # 该运动类型被创建时必须为真的条件（触发器）
    # Root = 国家
    creation_trigger = {} -- 创建触发器 = {}

    # 该运动类型相对于其他同时有效的运动类型被选中创建的权重
    # Root = 国家
    creation_weight = { -- 创建权重 = {
        value = 100 -- 值 = 100
    }

    # 当创建此类型的运动时执行的效果
    # Root = 政治运动本身
    on_created = {} -- 创建时 = {}

    # 选择文化作为该运动类型的文化身份时必须为真的条件（触发器），从国家中存在的文化中选择
    # root = 文化
    # scope:country = 运动将被创建的国家
    culture_selection_trigger = {} -- 文化选择触发器 = {}

    # 选择文化作为该运动类型的文化身份的权重，与国家中存在且对该运动类型有效的其他文化相比
    # root = 文化
    # scope:country = 运动将被创建的国家
    culture_selection_weight = {} -- 文化选择权重 = {}

    # 选择宗教作为该运动类型的宗教身份时必须为真的条件（触发器），从国家中存在的宗教中选择
    # root = 宗教
    # scope:country = 运动将被创建的国家
    religion_selection_trigger = {} -- 宗教选择触发器 = {}

    # 选择宗教作为该运动类型的宗教身份的权重，与国家中存在且对该运动类型有效的其他宗教相比
    # root = 宗教
    # scope:country = 运动将被创建的国家
    religion_selection_weight = {} -- 宗教选择权重 = {}

    # 鼓动者（agitator）能够支持此类运动的条件（触发器）
    # Root = 角色
    # scope:culture = 运动的文化身份（如果有）
    # scope:religion = 运动的宗教身份（如果有）
    # scope:interest_group = 运动所在国家中与该角色所属利益集团（IG）匹配的利益集团 - 使用这个而不是角色的实际IG，以便对流亡的鼓动者有效
    character_support_trigger = {} -- 角色支持触发器 = {}

    # 鼓动者支持此类运动的权重，与其他他们可以支持的有效运动相比
    # Root = 角色
    # scope:culture = 运动的文化身份（如果有）
    # scope:religion = 运动的宗教身份（如果有）
    character_support_weight = {} -- 角色支持权重 = {}

    # 运动能够向某个利益集团（IG）施压的条件（触发器）（除了所需的支持影响力（clout）之外）
    # Root = 利益集团
    can_pressure_interest_group = {} -- 可向利益集团施压 = {}

    # 人口（pop）中的个体能够支持此类运动的条件（触发器）
    # Root = 人口
    # scope:culture = 运动的文化身份（如果有）
    # scope:religion = 运动的宗教身份（如果有）
    pop_support_trigger = { -- 人口支持触发器 = {
        culture = {
            is_primary_culture_of = root.owner -- 是 root.owner（该人口所有者国家）的主流文化
        }
    }

    # 这些是将在该运动的UI中显示的人口支持因素 - 本身对游戏玩法没有直接影响
    # 人口支持因素在它们自己的数据库中定义
    pop_support_factors = {} -- 人口支持因素 = {}

    # 人口中的个体支持此类运动的权重，与其他他们可以支持的有效运动相比
    # Root = 人口
    # scope:culture = 运动的文化身份（如果有）
    # scope:religion = 运动的宗教身份（如果有）
    pop_support_weight = {} -- 人口支持权重 = {}

    # 关于该运动类型可以引发何种内战的配置数据
    # 如果某种类型未在此处明确编写脚本，则对该运动类型无效
    revolution/secession = { -- 革命/分离主义 = {
        # 该内战类型对该运动类型是否可能发生的条件（触发器）
        # Root = 政治运动本身
        # scope:clout = 将成为叛乱者的利益集团的总影响力（clout）
        possible = {} -- 可能发生 = {}

        # 选择该内战类型而非其他类型的权重
        # Root = 政治运动本身
        # scope:clout = 将成为叛乱者的利益集团的总影响力（clout）
        weight = {} -- 权重 = {}

        # 可选，可用于强制该类型的运动在叛乱时采用特定的国家标签（tag）
        forced_tags = { -- 强制标签 = {
            TAG = { # 应使用的国家定义/标签
                # 该标签是否有效的条件（触发器）
                # root = 政治运动本身
                trigger = { -- 触发器 = {
                    owner ?= { has_journal_entry = je_acw_countdown } -- 所有者是否拥有日记条目 je_acw_countdown
                }
                # 该标签被选中而非其他有效选项的权重
                weight = x -- 权重 = x
            }
        }

        # 决定哪些州倾向于加入内战一方的权重 - 如果为0，该州将永远是忠诚派
        # 请注意，还有其他因素会影响这一点，特别是对于具有文化/宗教身份的运动
        state_weight = { -- 州权重 = {
            value = 1 -- 值 = 1
            if = { -- 如果 = {
                limit = { -- 条件 = {
                    is_homeland_of_country_cultures = owner -- 是国家所有者文化组的家园
                }
                add = 50 -- 增加 = 50
            }
        }

        # 应加入内战方的国家州的目标比例
        # 如果未设置，将使用默认定义（defines）决定
        target_fraction_of_states = {} -- 目标州比例 = {}
    }

    # 乘数：影响法律颁布对该运动类型激进主义（radicalism）的影响
    law_enactment_radicalism_multiplier = x -- 法律颁布激进主义乘数 = x

    # 乘数：影响现行法律对该运动类型激进主义（radicalism）的影响
    active_law_radicalism_multiplier = x -- 现行法律激进主义乘数 = x

    # 用于增加/减少该运动类型激进主义（radicalism）的特定因素
    additional_radicalism_factors = {} -- 额外激进主义因素 = {}
}