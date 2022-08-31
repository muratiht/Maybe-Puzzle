const Discord = require('discord.js')
const db = require('croxydb')

exports.run = async (client, message, args) => {

    if(!message.member.permissions.has("Administrator")) return message.reply("Bu Komutu Kullanmak İçin **Yönetici** Yetkisine Sahip Olmalısın!");
//Tanımlar
let log = message.mentions.channels.first();
let logkanal = await db.get(`log_${message.guild.id}`)
    
  //Embedler
  const qyok = new Discord.EmbedBuilder().setTitle('İşlem başarısız.').setDescription('Öncelikle bir log kanalı ayarlamalısın.').setThumbnail(message.guild.iconURL()).setColor('Red')
  const qvar = new Discord.EmbedBuilder().setTitle('İşlem başarılı.').setDescription('Log kanalı başarıyla kaldırıldı.').setThumbnail(message.guild.iconURL()).setColor('White')
  const kyok = new Discord.EmbedBuilder().setTitle('İşlem başarısız.').setDescription('Log kanalı belirtiniz.').setThumbnail(message.guild.iconURL()).setColor('Red')
  const qnix = new Discord.EmbedBuilder().setTitle('İşlem başarılı.').setDescription('Log kanalı ayarlandı.').setThumbnail(message.guild.iconURL()).setColor('White')
  //

    if(args[0] === 'sıfırla' || args[0] === 'sil') {
    if(!logkanal) return message.channel.send({embeds : [qyok]})
      
    db.delete(`log_${message.guild.id}`)
    return message.channel.send({embeds : [qvar]})
    }
    if(!log) return message.channel.send({embeds : [kyok]})
    
    db.set(`log_${message.guild.id}`, log.id)
    message.channel.send({embeds : [qnix]});
};
    exports.conf = {
        aliases: ['log', 'mesaj-log'], 
      };
      
      exports.help = {
        name: 'mesajlog',
      };
