require 'yaml'

SETTING_YML = 'setting.yml'

def setting_for(setting_yml)
  YAML.load_file(setting_yml || SETTING_YML)
end

task default: :pi_from_regular_polygon

desc 'pi_from_regular_polygon'
task :pi_from_regular_polygon, [:setting_yml] do |task, args|
  setting = setting_for(args[:setting_yml])

  # 調べる最大の正多角形の角数
  max_n = setting['max_n']
  # 指定の角形まではスキップしない
  no_skip_until = setting['no_skip_until']
  # スキップする数
  skip = setting['skip']
  # 結果を出力するファイルパス
  out_csv = setting['out_csv']

  File.open(out_csv, 'w') do |out|
    pi_from_regular_polygon(max_n, skip, no_skip_until, out)
  end
end

def pi_from_regular_polygon(max_n = 100, skip = 1, no_skip_until = nil, out = STDOUT)
  puts "正三角形 → 正#{ max_n }角形 まで"
  puts '--'

  all_ns = (3..max_n).to_a

  no_skip_ns = if no_skip_until
    all_ns.select { |n| n <= no_skip_until }
  else
    []
  end

  slip_ns = (all_ns - no_skip_ns)
    .each_slice(skip)
    .map{ |ns| ns.last }
  
  target_ns = (no_skip_ns + slip_ns)

  target_ns.each do |n|
    res = pi_from_regular_polygon_for(n)
    out.puts("#{ n },#{ res[:si] },#{ res[:so] }")
  end
end

def pi_from_regular_polygon_for(n)
  t = 2 * Math::PI / n # 角度
  r = 1 # 半径

  # 内接する正多角形 inside
  hi = r * Math::sin(t) # 高さ
  si = (r * hi * 0.5) * n # 全面積

  # 外接する正多角形 outside
  ho = r * Math::tan(t * 0.5) # 高さ
  so = (r * ho * 0.5) * 2 * n # 全面積

  puts "正#{ n }角形では"
  puts si
  puts " ～"
  puts so
  puts "の間に π がある"
  puts '---'

  {
    n: n,
    si: si,
    so: so,
  }
end