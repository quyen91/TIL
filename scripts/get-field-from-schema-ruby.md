#### Get field + type from table in schema of rails app with ruby

```ruby
# @quyencv
# Get all fields from schema
# Example
#
# create_table "cards", options: "ENGINE=InnoDB DEFAULT CHARSET=utf8", force: :cascade do |t|
#   t.string "name"
#   t.integer "data_flg", default: 0
#   t.bigint "parent_id"
#   t.datetime "created_at", null: false
#   t.datetime "updated_at", null: false
# end
#
# Folder structure
# scripts/main.rb
# scripts/data.txt
# scripts/out.txt

# File: scripts/main.rb
def execute mode
  if mode == 'field'
    get_field()
  else
    get_type()
  end
end

def get_field
  fw = File.new('out.txt', 'w')

  File.open("data.txt", "r") do |f|
    f.each_line do |line|
      a = line.split(' ')[1]
      p a.gsub(/[",]/, '') unless a.nil?
      fw.puts(a.gsub(/[",]/, '')) unless a.nil?
    end
  end

  fw.close
end

def get_type
  fw = File.new('out.txt', 'w')

  File.open("data.txt", "r") do |f|
    f.each_line do |line|
      a = line.split(' ')[0]
      a = a.split('.')[1]
      fw.puts(a.gsub(/[",]/, '')) unless a.nil?
    end
  end

  fw.close
end

execute('field')
# execute('type')
```