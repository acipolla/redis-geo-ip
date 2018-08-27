require 'redis'
require 'ipaddr'
loc= Hash.new
country = Hash.new
redis=Redis.new
File.readlines('GeoLite2-Country-Locations-en.csv').each do |riga|
line=riga.split(',')
nome= !line[5].nil? ? line[5] : line[3]
country.merge!(line[0]=>nome.unpack("U*").map{|c|c.chr}.join.tr('"',''))
end
File.readlines('GeoLite2-Country-Blocks-IPv4.csv').each do |riga|
  line=riga.split(',')
ip=line[0].split('/')[0]
if !loc.key?(line[1])
  loc.merge!(line[1]=>[ip])
else
  loc[line[1]] << ip
end
end
i=0
loc.each do |k,a|
redis.zadd('country',i,country[k])
a.each do |x|
  redis.zadd("ip",IPAddr.new(x).to_i,i)
  i+=1
end
end
